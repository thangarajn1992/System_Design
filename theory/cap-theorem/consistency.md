# Consistency

With multiple copies of the same data, we are faced with options on how to synchronize them so clients have a consistent view of the data. Recall the definition of consistency from the [CAP theorem](https://app.gitbook.com/s/-MiN5WEILfEyFwyPsayW/\~/changes/F8xkSimMmZoTZmlAtD2Q/theory/cap-theorem) - Every read receives the most recent write or an error.

## Consistency Patterns

### Weak consistency

After a write, reads may or may not see it. A best effort approach is taken.

This approach is seen in systems such as mem-cached. Weak consistency works well in real time use cases such as VoIP, video chat, and real-time multiplayer games. For example, if you are on a phone call and lose reception for a few seconds, when you regain connection you do not hear what was spoken during connection loss.

### Eventual consistency

After a write, reads will eventually see it (typically within milliseconds). Data is replicated asynchronously.

This approach is seen in systems such as DNS and email. Eventual consistency works well in highly available systems.

### Strong consistency

After a write, reads will see it. Data is replicated synchronously.

This approach is seen in file systems and RDBMSes. Strong consistency works well in systems that need transactions.
