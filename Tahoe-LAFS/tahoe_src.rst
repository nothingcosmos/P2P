tahoe-lafs
###############################################################################

easy_install allmydata-tahoe

依存ライブラリ

# Twisted
# zope
# lscap
# zfec
# pycryptopp
# pyutil


tahoe-lafs/src/allmydata

src ::

  __init__.py
  _appname.py
  _auto_deps.py
  _version.py
  blacklist.py
      blocklistを管理する。ファイルはblocklistに分割して、同時に転送するはず。親はhash-treeかな。
      他にも、prohibitedNode prohibitedFileが存在している。
  check_results.py
  client.py
  codec.py
  control.py
  debugshell.py
  dirnode.py
  hashtree.py
      Merkle hashes
  history.py
  interfaces.py
  key_generator.py
  manhole.py
  monitor.py
  node.py
  nodemaker.py
  stats.py
  storage_client.py
  unknown.py
  uri.py
  webish.py

  frontends
    __init__.py
    auth.py
    drop_upload.py
    ftpd.py
    sftpd.py
  immutable
    __init__.py
    checker.py
    downloader
      __init__.py
      common.py
      fetcher.py
      finder.py
      node.py
      segmentation.py
      share.py
      status.py
    encode.py
    filenode.py
    layout.py
    literal.py
    offloaded.py
    repairer.py
    upload.py
  introducer
    __init__.py
    client.py
    common.py
    interfaces.py
    old.py
    server.py
  mutable
    __init__.py
    checker.py
    common.py
    filenode.py
    layout.py
    publish.py
    repairer.py
    retrieve.py
    servermap.py
  scripts
    __init__.py
    admin.py
    backupdb.py
    cli.py
    common.py
    common_http.py
    create_node.py
    debug.py
    keygen.py
    runner.py
    slow_operation.py
    startstop_node.py
    stats_gatherer.py
    tahoe_add_alias.py
    tahoe_backup.py
    tahoe_check.py
    tahoe_cp.py
    tahoe_get.py
    tahoe_ls.py
    tahoe_manifest.py
    tahoe_mkdir.py
    tahoe_mv.py
    tahoe_put.py
    tahoe_unlink.py
    tahoe_webopen.py
  storage
    __init__.py
    common.py
    crawler.py
    expirer.py
    immutable.py
    lease.py
    mutable.py
    server.py
    shares.py
  test
  util
    __init__.py
    abbreviate.py
    assertutil.py
    base32.py
    base62.py
    cachedir.py
    consumer.py
    deferredutil.py
    dictutil.py
    encodingutil.py
    fake_inotify.py
    fileutil.py
    happinessutil.py
    hashutil.py
    humanreadable.py
    idlib.py
    iputil.py
    keyutil.py
    limiter.py
    log.py
    mathutil.py
    netstring.py
    nummedobj.py
    observer.py
    pipeline.py
    pkgresutil.py
    pollmixin.py
    repeatable_random.py
    rrefutil.py
    sibpath.py
    spans.py
    statistics.py
    time_format.py
    verlib.py
  web
    __init__.py
    check-and-repair-results.xhtml
    check-results.xhtml
    check_results.py
    common.py
    deep-check-and-repair-results.xhtml
    deep-check-results.xhtml
    directory.py
    directory.xhtml
    download-status-timeline.xhtml
    download-status.xhtml
    filenode.py
    helper.xhtml
    info.py
    info.xhtml
    introducer.xhtml
    introweb.py
    literal-check-results.xhtml
    manifest.xhtml
    map-update-status.xhtml
    operations.py
    publish-status.xhtml
    rename-form.xhtml
    retrieve-status.xhtml
    root.py
    static
    statistics.xhtml
    status.py
    status.xhtml
    storage.py
    storage_status.xhtml
    unlinked.py
    upload-results.xhtml
    upload-status.xhtml
    welcome.xhtml
  windows
    __init__.py
    fixups.py
    registry.py
    tahoesvc.py


introducer
*******************************************************************************

i/f ::

  publish()
  subscribe_to()

  connected_to_introducer()


duplicate_announcement

hashに突っ込んでindexが重複すれば duplicateをかえす


storage
*******************************************************************************

crawlerにおいて
process_bucket のタイミングでduplicateしているkも


===============================================================================


===============================================================================


*******************************************************************************

===============================================================================
===============================================================================
===============================================================================
===============================================================================
===============================================================================
===============================================================================



*******************************************************************************
===============================================================================
===============================================================================
