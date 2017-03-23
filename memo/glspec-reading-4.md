# Event Model 

### Sync Objects and Fences 

 A sync object acts as a synchronization primitive – a representation of events whose completion status can be tested or waited upon.
 
Sync objects have a status value with two possible states: signaled and unsignaled. Events are associated with a sync object. When a sync object is cre-
ated, its status is set to unsignaled. When the associated event occurs, the sync object is signaled (its status is set to signaled).

    sync FenceSync( enum condition, bitfield ﬂags );

The command creates a new fence sync object, inserts a fence command in the GL command stream and associates it with that sync object, and returns a non-zero name corre-
sponding to the sync object.

When the speciﬁed condition of the sync object is satisﬁed by the fence command, the sync object is signaled by the GL, causing any ClientWaitSync or Wait-
Sync commands (see below) blocking on sync to unblock. No other state is affected by FenceSync or by execution of the associated fence command.

condition must be SYNC_GPU_COMMANDS_COMPLETE. This condition is satisﬁed by completion of the fence command corresponding to the sync object and all
preceding commands in the same command stream. The sync object will not be signaled until all effects from these commands on GL client and server state and the
framebuffer are fully realized. 

A sync object can be deleted by passing its name to the command: 

    void DeleteSync( sync sync );

If the fence command corresponding to the speciﬁed sync object has completed, or if no ClientWaitSync or WaitSync commands are blocking on sync, the
object is deleted immediately. Otherwise, sync is ﬂagged for deletion and will be deleted when it is no longer associated with any fence command and is no longer
blocking any ClientWaitSync or WaitSync command. 

    enum ClientWaitSync( sync sync, bitfield ﬂags,uint64 timeout );

The command causes the GL to block, and will not return until the sync object sync is signaled, or until the speciﬁed timeout period expires.

ClientWaitSync returns one of four status values. A return value of ALREADY_SIGNALED indicates that sync was signaled at the time ClientWait-
Sync was called. ALREADY_SIGNALED will always be returned if sync was signaled, even if the value of timeout is zero. A return value of TIMEOUT_EXPIRED
indicates that the speciﬁed timeout period expired before sync was signaled. A return value of CONDITION_SATISFIED indicates that sync was signaled before the
timeout expired. Finally, if an error occurs, in addition to generating a GL error as speciﬁed below, ClientWaitSync immediately returns WAIT_FAILED without
blocking.

    void WaitSync( sync sync, bitfield ﬂags, uint64 timeout ); 
    
The command is similar to ClientWaitSync, but instead of blocking and not returning to the application until sync is signaled, WaitSync returns immediately, instead causing the
GL server to block until sync is signaled.

`timeout` must currently be the special value TIMEOUT_IGNORED, and is not used. Instead, WaitSync will always wait no longer than an implementation-dependent timeout. The duration of this timeout in nanoseconds may be queried by calling GetInteger64v with pname MAX_SERVER_WAIT_TIMEOUT. There is currently no way to determine whether WaitSync unblocked because the timeout expired or because the sync object being waited on was signaled.

If an error occurs, WaitSync generates a GL error as speciﬁed below, and does not cause the GL server to block.

#### Signaling
If the sync object being blocked upon will not be signaled in ﬁnite time (for example, by an associated fence command issued previously, but not yet ﬂushed
to the graphics pipeline), then ClientWaitSync may hang forever. To help prevent this behavior,if ClientWaitSync is called and all of the following are true:

- the SYNC_FLUSH_COMMANDS_BIT bit is set in ﬂags
- sync is unsignaled when ClientWaitSync is called
- and the calls to ClientWaitSync and FenceSync were issued from the same context

then the GL will behave as if the equivalent of Flush were inserted immediately after the creation of sync.

#### Sync Object Queries 

Properties of sync objects may be queried using the command

    void GetSynciv( sync sync, enum pname, sizei bufSize, sizei *length, int *values );
    
The command

    boolean IsSync( sync sync );
    
returns TRUE if sync is the name of a sync object. If sync is not the name of a sync object, or if an error condition occurs, IsSync returns FALSE (note that zero is not
the name of a sync object).

Sync object names immediately become invalid after calling DeleteSync, as discussed prviously , but the underlying sync object will not be deleted
until it is no longer associated with any fence command and no longer blocking any *WaitSync command.

### Query Objects and Asynchronous Queries 

Asynchronous queries provide a mechanism to return information about the processing of a sequence of GL commands.

### Time Queries 

Query objects may also be used to track the amount of time needed to fully complete a set of GL commands (a time elapsed query), or to determine the current time of the GL (a timer query).

When BeginQuery and EndQuery are called with a target of TIME_ELAPSED, the GL prepares to start and stop the timer used for time elapsed queries. The timer is started or stopped when the effects from all previous commands on the GL client
and server state and the framebuffer have been fully realized. The BeginQuery and EndQuery commands may return before the timer is actually started or stopped. When the time elapsed query timer is ﬁnally stopped, the elapsed time (in nanoseconds) is written to the corresponding query object as the query result value, and the query result for that object is marked as available.
