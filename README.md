# Linux-dvb-apps-for-ARM

It's assumed you installed gcc arm; But if you didn't:
```javascript
sudo apt-get install gcc-arm-linux-gnueabi sudo apt-get install g++-arm-linux-gnueabi sudo apt-get install build-essential
```
Then clone linux-dvb-apps source code:
```javascript
hg clone http://linuxtv.org/hg/dvb-apps
```
Now you should edit linux-dvb-apps Make.rules to add cross-compile feature to it; To do that, find all of '$(CC)', and add $(CROSS) before them.
For example
```javascript
  %.o: %.c
	  $(CC) -c $(CPPFLAGS) $(CFLAGS) -MMD -o $@ $< $(filter-out %.h %.c,$^)
```	
to
```javascript
  %.o: %.c
	  $(CROSS)$(CC) -c $(CPPFLAGS) $(CFLAGS) -MMD -o $@ $< $(filter-out %.h %.c,$^)
```	
Find result number should be 8 probably.
Now time to compile:
```javascript
  make sattic=1 CROSS=arm-linux-gnueabi-g
```
*Note:
static=1          - Build all applications statically.

And finally for install:
```javascript
  make install=/path/to/your/destination/dvb-apps-arm-statically
```
