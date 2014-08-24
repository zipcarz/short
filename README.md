short
=====

...	...	@@ -118,7 +118,8 @@ std::map<Address,AddressData> BanWatcher::addressData;
118	118	 extern "C" {
119	119	   static void sighup_handler(int sig) {
120	120	     int save_errno = errno;
121		-    write(signal_pipe[1], &sig, 1);
121	+    int rc = write(signal_pipe[1], &sig, 1);
122	+    (void) rc;
122	123	     errno = save_errno;
123	124	   }
124	125	 }
...	...	@@ -275,8 +276,8 @@ int main(int argc, char **argv) {
275	276	         // Check for signals
276	277	         if(FD_ISSET(signal_pipe[0], &fds)) {
277	278	           char drain[4];
278		-          read(signal_pipe[0], drain, sizeof drain);
279		-            ;
279	+          int rc = read(signal_pipe[0], drain, sizeof drain);
280	+          (void)rc;
280	281	           break;
281	282	         }
282	283	       }
