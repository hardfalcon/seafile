
AM_CFLAGS = -DPKGDATADIR=\"$(pkgdatadir)\" \
	-DPACKAGE_DATA_DIR=\""$(pkgdatadir)"\" \
	-I$(top_srcdir)/include \
	-I$(top_srcdir)/lib \
	-I$(top_srcdir)/common \
	@CCNET_CFLAGS@ \
	@SEARPC_CFLAGS@ \
	@GLIB2_CFLAGS@ \
	@MSVC_CFLAGS@ \
	-Wall

bin_PROGRAMS = 
if !SERVER_ONLY
bin_PROGRAMS += seaf-daemon
endif

proc_headers = $(addprefix processors/, \
	check-tx-proc.h \
	check-tx-v2-proc.h \
	getcommit-proc.h \
	sendcommit-proc.h \
	sendfs-proc.h \
	getfs-proc.h \
	getblock-proc.h \
	getblock-v2-proc.h \
	sendblock-proc.h \
	sendblock-v2-proc.h \
	sendbranch-proc.h \
	getcs-proc.h \
	sync-repo-proc.h \
	notifysync-proc.h \
	notifysync-slave-proc.h \
	sync-repo-slave-proc.h \
	check-tx-slave-proc.h \
	putcommit-proc.h  \
	putfs-proc.h \
	getcommit-v2-proc.h \
	sendcommit-v2-proc.h \
	sendcommit-v3-proc.h \
	getrepoemailtoken-proc.h )

noinst_HEADERS = \
	repo-mgr.h \
	transfer-mgr.h \
	status.h sync-mgr.h  \
	wt-monitor.h \
	merge.h merge-recursive.h vc-utils.h seafile-session.h \
	clone-mgr.h \
	$(proc_headers)

if LINUX
wt_monitor_src = wt-monitor-linux.c
endif

if WIN32
wt_monitor_src = wt-monitor-win32.c
endif

if MACOS
wt_monitor_src = wt-monitor-macos.c
endif

common_src = \
	transfer-mgr.c \
	../common/unpack-trees.c ../common/seaf-tree-walk.c \
	merge.c merge-recursive.c vc-utils.c \
	status.c sync-mgr.c seafile-session.c \
	../common/seafile-crypt.c ../common/diff-simple.c $(wt_monitor_src) \
	seaf-ext.c clone-mgr.c \
	../common/seafile-config.c ../common/bitfield.c \
	../common/branch-mgr.c ../common/fs-mgr.c \
	repo-mgr.c ../common/commit-mgr.c \
	../common/log.c ../common/avl/avl.c ../common/object-list.c \
	../common/rpc-service.c \
	../common/gc.c ../common/vc-common.c \
	../common/seaf-utils.c \
	../common/obj-store.c \
	../common/obj-backend-fs.c \
	../common/block-mgr.c \
	../common/block-backend.c \
	../common/block-backend-fs.c \
	../common/mq-mgr.c \
	processors/check-tx-proc.c \
	processors/check-tx-v2-proc.c \
	processors/getcommit-proc.c \
	processors/sendcommit-proc.c \
	processors/sendfs-proc.c \
	processors/getfs-proc.c \
	processors/getblock-proc.c \
	processors/getblock-v2-proc.c \
	processors/sendblock-proc.c \
	processors/sendblock-v2-proc.c \
	processors/sendbranch-proc.c \
	processors/getcs-proc.c \
	processors/notifysync-proc.c \
	processors/notifysync-slave-proc.c \
	processors/sync-repo-proc.c \
	processors/sync-repo-slave-proc.c \
	processors/check-tx-slave-proc.c \
	processors/putcommit-proc.c \
	processors/putfs-proc.c \
	processors/getcommit-v2-proc.c \
	processors/sendcommit-v2-proc.c \
	processors/sendcommit-v3-proc.c \
	processors/getrepoemailtoken-proc.c


seaf_daemon_SOURCES = seaf-daemon.c $(common_src)

seaf_daemon_LDADD = @CCNET_LIBS@ \
	@LIB_INTL@ \
	$(top_builddir)/lib/libseafile_common.la \
	@GLIB2_LIBS@  @GOBJECT_LIBS@ -lssl @LIB_RT@ @LIB_UUID@ -lsqlite3 -levent \
	$(top_builddir)/common/cdc/libcdc.la \
	$(top_builddir)/common/index/libindex.la ${LIB_WS32} \
	@SEARPC_LIBS@ @LIB_DIRWATCH@

seaf_daemon_LDFLAGS = @STATIC_COMPILE@ @CONSOLE@

# seaf_tool_CFLAGS = $(AM_CFLAGS) -DSEAF_TOOL

# seaf_tool_SOURCES = seaf-tool.c $(common_src) 

# seaf_tool_LDADD = $(seaf_daemon_LDADD)

# seaf_tool_LDFLAGS = @STATIC_COMPILE@ # @CONSOLE@

check_PROGRAMS = seaf-test

seaf_test_SOURCES = \
	seaf-test.c transfer-mgr.c \
	merge.c merge-recursive.c vc-utils.c \
	status.c sync-mgr.c seafile-session.c \
	../common/seafile-crypt.c ../common/diff-simple.c ${wt_monitor_src} \
	../common/seafile-config.c ../common/bitfield.c seaf-ext.c clone-mgr.c \
	../common/branch-mgr.c ../common/fs-mgr.c \
	repo-mgr.c ../common/commit-mgr.c \
	../common/log.c ../common/avl/avl.c ../common/object-list.c \
	../common/rpc-service.c \
	../common/gc.c ../common/vc-common.c ../common/seaf-utils.c \
	../common/unpack-trees.c ../common/seaf-tree-walk.c \
	../common/mq-mgr.c \
	../common/obj-store.c \
	../common/obj-backend-fs.c \
	../common/block-mgr.c \
	../common/block-backend.c \
	../common/block-backend-fs.c \
	processors/check-tx-proc.c \
	processors/getcommit-proc.c \
	processors/sendcommit-proc.c \
	processors/sendfs-proc.c \
	processors/getfs-proc.c \
	processors/getblock-proc.c \
	processors/sendblock-proc.c \
	processors/sendbranch-proc.c \
	processors/getcs-proc.c \
	processors/notifysync-proc.c \
	processors/notifysync-slave-proc.c \
	processors/sync-repo-proc.c \
	processors/getcommit-v2-proc.c \
	processors/sendcommit-v2-proc.c

seaf_test_CPPFLAGS = -DDEBUG_UNPACK_TREES -DSEAF_TEST
seaf_test_LDADD = @CCNET_LIBS@ \
	@LIB_INTL@ \
	$(top_builddir)/lib/libseafile_common.la \
	@GLIB2_LIBS@  @GOBJECT_LIBS@ -lssl @LIB_RT@ @LIB_UUID@ -lsqlite3 -levent \
	$(top_builddir)/common/cdc/libcdc.la \
	$(top_builddir)/common/index/libindex.la ${LIB_WS32} \
	@SEARPC_LIBS@ @LIB_DIRWATCH@

seaf_test_LDFLAGS = @STATIC_COMPILE@  @CONSOLE@

#TESTS = seaf-test