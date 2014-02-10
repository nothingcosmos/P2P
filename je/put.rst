put
###############################################################################

putのリスト
*******************************************************************************

grpe put * | grep public ::

  Cursor.java:    public OperationStatus put(final DatabaseEntry key,
  Cursor.java:    public OperationStatus putNoOverwrite(final DatabaseEntry key,
  Cursor.java:    public OperationStatus putNoDupData(final DatabaseEntry key,
  Cursor.java:    public OperationStatus putCurrent(final DatabaseEntry data)
  Database.java:    public OperationStatus put(final Transaction txn,
  Database.java:    public OperationStatus putNoOverwrite(final Transaction txn,
  Database.java:    public OperationStatus putNoDupData(final Transaction txn,
  DbInternal.java:    public static OperationStatus putForReplay
  SecondaryCursor.java:    public OperationStatus put(final DatabaseEntry key,
  SecondaryCursor.java:    public OperationStatus putNoOverwrite(final DatabaseEntry key,
  SecondaryCursor.java:    public OperationStatus putNoDupData(final DatabaseEntry key,
  SecondaryCursor.java:    public OperationStatus putCurrent(final DatabaseEntry data) {
  SecondaryDatabase.java:    public OperationStatus put(final Transaction txn,
  SecondaryDatabase.java:    public OperationStatus putNoOverwrite(final Transaction txn,
  SecondaryDatabase.java:    public OperationStatus putNoDupData(final Transaction txn,


===============================================================================
===============================================================================



===============================================================================
===============================================================================


put
*******************************************************************************

Database.java ::

  put
    putInternal(Transaction, DatabaseEntry, DatabaseEntry, PutMode)
      locker = LockerFactory.getWritableLocker
      cursor = new Cursor(this, locker, null)
      cursor.putInternal(key, data, putMode)

Cursor.java ::

  putInternal()
    synchronized (getTxnSynchronizer())
      if (dbImpl.getSortedDuplicates())
        return putHandleDups(key, data, putMode)
      return putNoDups(key, data, putMode)

  putHandleDups()
    switch
      OVERWRITE
      NO_OVERWRITE
      NO_DUP_DATA
      CURRENT


  putNoDups()
    putNotify(key, data, ln, putode, dbImpl.getRepContext())
      Key.makeKey(key)
        key.setData()

      dbHandle.setAssoc.getSecondaries(key)
      SecondaryDatabase.needOldDataForUpdate()

      putCurrentNoNotify()
        cursorImpl.putCurrent()
      putNoNotify()
        putAllowPhantoms()
          dup = beginMoveCursor()
          dup.put()


dbi/CursorImpl.java ::

  put()
    putInternal()
      databaseImpl.getTree().findBinForInsert(key, this)
        insertNewSlot()
      getSlotReuseInfo()
        putCurrentAlreadyLatchedAndLocked()

  putCurrent()
    putCurrentAlreadyLatchedAndLocked()
      bin.fetchTarget(index)
      bin.updateNode(index, xxx)

      if bin.getTarget(index)
        bin.evictLN(index)
          evictInternal()

      finnaly releaseBIN


com.sleepycat.je.tree.BIN BINBoundary
===============================================================================

A BIN represents a Bottom Internal Node in the JE tree.

tree/BIN.java ::

  BIN extends IN implements Loggable

  evictInternal()
    Node getTarget(index)
    isEvictable(lsn)
      cleaner.isEvictable()
      logDirtyLN()
      setTarget(index,


Node fetchTarget(index)


VLSNCache

perhaps VLSN caching, Sequence

VLSNCache

Versioned sequence for the LN Leaf Node

LN is Leaf Node

そもそもLSNとは

Log Sequence Number

utilint/VLSN

  /**
   * VersionedLN is used to  provide an in-memory representation of an LN that
   * makes its VLSN available through btree access.
   *
   * On disk, each log entry is composed of a header (je.log.LogEntryHeader) and
   * a body (je.log.entry.LogEntry). When an LN is materialized in the Btree, it
   * usually holds only the body, and does not have access to information in the
   * log entry header, such as the VLSN. Since version based API operations need
   * access to the VLSN, environments which are configured with
   * je.rep.preserveRecordVersion=true instantiate VersionedLNs instead of LNs,
   * in order to cache the VLSN with the LN, and make it cheaply available to
   * Btree operations. 
  */

LeafNode

Version Sequence


===============================================================================

*******************************************************************************


DbTree.java
===============================================================================

 * For example, suppose we have two databases, foo and bar. We have the
 * following structure:
 *
 *           nameDatabase                          idDatabase
 *               IN                                    IN
 *                |                                     |
 *               BIN                                   BIN
 *    +-------------+--------+            +---------------+--------+
 *  .               |        |            .               |        |
 * NameLNs         NameLN    NameLN      MapLNs for   MapLN        MapLN
 * for internal    key=bar   key=foo     internal dbs key=53       key=79
 * dbs             data=     data=                    data=        data=
 *                 dbId79    dbId53                   DatabaseImpl DatabaseImpl
 *                                                        |            |
 *                                                   Tree for foo  Tree for bar
 *                                                        |            |
 *                                                     root IN       root IN
 *




===============================================================================

template ::
  ###############################################################################
  *******************************************************************************
  ===============================================================================

