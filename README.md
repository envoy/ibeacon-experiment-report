# iBeacon not working with iPhone issue investigation report

## Methodology

To make collecting data easily, we have three projects

 - https://github.com/envoy/ibeacon-experiment-ipad As the iBeacon signal source (the one broadcasts)
 - https://github.com/envoy/ibeacon-experiment-iphone As the iBeacon signal receiver
 - https://github.com/envoy/ibeacon-experiment-api As a simple REST API for collecting data
 
All the logs will be written into `NSUserDefaults` and then syn to the API server. In this way, even if we encounter networking issue, the log will still persist and eventually uploaded to server at some point. The code we wrote for iBeacon broadcasting and monitoring, we did our best to keep the code as simple as possible to avoid any potential side effects.

To be sure the iPad does the iBeacon broadcasting correctly, we use [iBeaconScanner](https://github.com/liamnichols/iBeaconScanner) to see if the iBeacon signal is really be broadcasting correctly.

![iBeaconScanner](/Screen Shot 2017-02-17 at 4.07.37 PM.png?raw=true "iBeaconScanner")

The physical setup is very simple, just put the broadcasting iPad on an iPad stand with "thi sis fine" dog by its side, and the other devices are laying on table.

![Physical setup](/IMG_9715.JPG?raw=true "Physical setup")

## Manual testing with scenarios

We registered users on our simple REST API server representing as different roles in the testing. Here's the users

 - User 1:
   - Role: iBeacon signal source
   - Device: iPad Air (Wi-Fi Only)
   - Model: MD788LL/B
   - OS: 10.2.1
 - User 2:
   - Role: iBeacon signal receiver
   - Device: iPhone 6s 64GB (Unlocked)
   - Model: MKRJ2LL/A
   - OS: 10.2.1
 - User 3:
   - Role: iBeacon signal receiver
   - Device: 1iPad mini 16 GB (Wi-Fi Only/1st Gen)
   - Model: MD528TA/A
   - OS: 9.3.4
   
To simulate entering iBeacon region, we make the iPad app active, it will then broadcast iBeacon signals. To simulate leaving iBeacon region, we make the iPad app goes into background, then it will stop broadcasting.

### Display off

Both iPad mini and iPhone are unplugged.


1. Enter region - Works ✅

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-enter-foreground</td>
			<td>app will enter foreground</td>
			<td>2017-02-21 21:48:17.449+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>did-enter-region</td>
			<td>did enter region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 21:48:17.634+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-become-active</td>
			<td>app did become active</td>
			<td>2017-02-21 21:48:17.898+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x156b3ef0> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=9.3.4, systemUpTime=6442.638657125, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
			<td>2017-02-21 21:48:20.515+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>did-enter-region</td>
			<td>did enter region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x1568ac30> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 21:48:20.556+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-21 21:48:20.56+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-21 21:48:20.565+00</td>
		</tr>
	</table>

2. Exit region - Works ✅

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-resign-active</td>
			<td>app will resign active</td>
			<td>2017-02-21 21:49:58.97+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-enter-background</td>
			<td>app did enter background</td>
			<td>2017-02-21 21:49:59.666+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>did-exit-region</td>
			<td>did exit region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 21:50:34.339+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>did-exit-region</td>
			<td>did exit region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x155eb590> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 21:50:38.847+00</td>
		</tr>
	</table>

3. Enter region - Works ✅

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-enter-foreground</td>
			<td>app will enter foreground</td>
			<td>2017-02-21 21:55:30.631+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-become-active</td>
			<td>app did become active</td>
			<td>2017-02-21 21:55:31.053+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>did-enter-region</td>
			<td>did enter region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 21:55:31.3+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>did-enter-region</td>
			<td>did enter region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x15677380> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 21:55:31.838+00</td>
		</tr>
	</table>

4. Exit region - Works ✅

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-resign-active</td>
			<td>app will resign active</td>
			<td>2017-02-21 21:56:03.974+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-enter-background</td>
			<td>app did enter background</td>
			<td>2017-02-21 21:56:04.663+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>did-exit-region</td>
			<td>did exit region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 21:56:37.412+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>did-exit-region</td>
			<td>did exit region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x155ed1b0> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 21:56:43.02+00</td>
		</tr>
	</table>

5. Enter region - Works ✅

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-enter-foreground</td>
			<td>app will enter foreground</td>
			<td>2017-02-21 21:57:38.285+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-become-active</td>
			<td>app did become active</td>
			<td>2017-02-21 21:57:38.669+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>did-enter-region</td>
			<td>did enter region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 21:57:38.675+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>did-enter-region</td>
			<td>did enter region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x155c83a0> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 21:57:38.725+00</td>
		</tr>
	</table>

6. Exit region - Works ✅

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-resign-active</td>
			<td>app will resign active</td>
			<td>2017-02-21 21:58:15.282+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-enter-background</td>
			<td>app did enter background</td>
			<td>2017-02-21 21:58:15.947+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>did-exit-region</td>
			<td>did exit region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 21:58:49.352+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>did-exit-region</td>
			<td>did exit region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x155d8ec0> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 21:58:55.736+00</td>
		</tr>
	</table>

7. Enter region - Works ✅

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>3</td>
			<td>did-enter-region</td>
			<td>did enter region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x156ca200> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:00:01.773+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-enter-foreground</td>
			<td>app will enter foreground</td>
			<td>2017-02-21 22:00:01.879+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-become-active</td>
			<td>app did become active</td>
			<td>2017-02-21 22:00:02.264+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>did-enter-region</td>
			<td>did enter region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:00:02.336+00</td>
		</tr>
	</table>

8. Exit region - Works ✅

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-resign-active</td>
			<td>app will resign active</td>
			<td>2017-02-21 22:01:12.605+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-enter-background</td>
			<td>app did enter background</td>
			<td>2017-02-21 22:01:13.288+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>did-exit-region</td>
			<td>did exit region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:01:46.142+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>did-exit-region</td>
			<td>did exit region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x155eba30> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:01:52.733+00</td>
		</tr>
	</table>

9. Enter region - Works ✅

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-enter-foreground</td>
			<td>app will enter foreground</td>
			<td>2017-02-21 22:02:45.072+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-become-active</td>
			<td>app did become active</td>
			<td>2017-02-21 22:02:45.482+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>did-enter-region</td>
			<td>did enter region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x156dc870> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:02:45.693+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>did-enter-region</td>
			<td>did enter region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:02:46.074+00</td>
		</tr>
	</table>

10. Exit region - Works ✅

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-resign-active</td>
			<td>app will resign active</td>
			<td>2017-02-21 22:03:10.386+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-enter-background</td>
			<td>app did enter background</td>
			<td>2017-02-21 22:03:11.061+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>did-exit-region</td>
			<td>did exit region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:03:44.196+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>did-exit-region</td>
			<td>did exit region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x156de000> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:04:04.694+00</td>
		</tr>
	</table>

### Display off + App killed

Both iPad mini and iPhone are unplugged, the app is killed everytime before we run either entering and exiting region test. Interestingly we found that the app won't be shown in active app list (double tapping home button), you need to tap on the app icon so that it will be shown in the list and therefore can be killed.

1. Enter region - Works ✅

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-enter-foreground</td>
			<td>app will enter foreground</td>
			<td>2017-02-21 22:13:55.182+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-become-active</td>
			<td>app did become active</td>
			<td>2017-02-21 22:13:55.565+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=10.2.1, systemUpTime=210922.996781792, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
			<td>2017-02-21 22:13:55.667+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>did-enter-region</td>
			<td>did enter region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:13:55.729+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-21 22:13:55.75+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-21 22:13:55.755+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x17e9ec50> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=9.3.4, systemUpTime=6820.90521525, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
			<td>2017-02-21 22:13:56.301+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>did-enter-region</td>
			<td>did enter region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x17eadc50> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:13:56.414+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-21 22:13:56.42+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-21 22:13:56.441+00</td>
		</tr>
	</table>

2. Exit region - Works ✅

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-resign-active</td>
			<td>app will resign active</td>
			<td>2017-02-21 22:15:38.948+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-enter-background</td>
			<td>app did enter background</td>
			<td>2017-02-21 22:15:39.622+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=10.2.1, systemUpTime=211057.329768458, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
			<td>2017-02-21 22:16:09.982+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>did-exit-region</td>
			<td>did exit region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:16:10.02+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-21 22:16:10.038+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-21 22:16:10.043+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x1467ccf0> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=9.3.4, systemUpTime=6944.85695408333, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
			<td>2017-02-21 22:16:17.769+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>did-exit-region</td>
			<td>did exit region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x145530d0> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:16:17.788+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-21 22:16:17.801+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-21 22:16:17.81+00</td>
		</tr>
	</table>

3. Enter region - Works ✅

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-enter-foreground</td>
			<td>app will enter foreground</td>
			<td>2017-02-21 22:18:23.302+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-become-active</td>
			<td>app did become active</td>
			<td>2017-02-21 22:18:23.716+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=10.2.1, systemUpTime=211191.130388542, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
			<td>2017-02-21 22:18:23.782+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>did-enter-region</td>
			<td>did enter region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:18:23.864+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-21 22:18:23.874+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-21 22:18:23.877+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x17686340> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=9.3.4, systemUpTime=7026.36776329167, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
			<td>2017-02-21 22:18:24.381+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>did-enter-region</td>
			<td>did enter region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x1754e0d0> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:18:24.436+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-21 22:18:24.446+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-21 22:18:24.45+00</td>
		</tr>
	</table>

4. Exit region - Works ✅

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-resign-active</td>
			<td>app will resign active</td>
			<td>2017-02-21 22:19:55.856+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-enter-background</td>
			<td>app did enter background</td>
			<td>2017-02-21 22:19:56.532+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x15eb2c90> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=9.3.4, systemUpTime=7067.0934625, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
			<td>2017-02-21 22:20:36.336+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>did-exit-region</td>
			<td>did exit region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x15d64580> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:20:36.369+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-21 22:20:36.38+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-21 22:20:36.387+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=10.2.1, systemUpTime=211324.210621208, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
			<td>2017-02-21 22:20:36.86+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>did-exit-region</td>
			<td>did exit region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:20:36.931+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-21 22:20:36.935+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-21 22:20:36.938+00</td>
		</tr>
	</table>

5. Enter region - Works ✅

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-enter-foreground</td>
			<td>app will enter foreground</td>
			<td>2017-02-21 22:25:07.437+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-become-active</td>
			<td>app did become active</td>
			<td>2017-02-21 22:25:07.819+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=10.2.1, systemUpTime=211470.238165417, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
			<td>2017-02-21 22:25:07.874+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>did-enter-region</td>
			<td>did enter region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:25:07.944+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-21 22:25:07.949+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-21 22:25:07.953+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x16db1eb0> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=9.3.4, systemUpTime=7103.26784479167, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
			<td>2017-02-21 22:25:09.371+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>did-enter-region</td>
			<td>did enter region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x16dbc1d0> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:25:09.451+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-21 22:25:09.465+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-21 22:25:09.475+00</td>
		</tr>
	</table>

6. Exit region - Works ✅

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-resign-active</td>
			<td>app will resign active</td>
			<td>2017-02-21 22:27:39.503+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-enter-background</td>
			<td>app did enter background</td>
			<td>2017-02-21 22:27:40.181+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x14da3f10> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=9.3.4, systemUpTime=7157.45205608333, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
			<td>2017-02-21 22:28:19.365+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>did-exit-region</td>
			<td>did exit region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x14ed7680> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:28:19.396+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-21 22:28:19.408+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-21 22:28:19.422+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=10.2.1, systemUpTime=211662.843866167, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
			<td>2017-02-21 22:28:20.487+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>did-exit-region</td>
			<td>did exit region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:28:20.537+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-21 22:28:20.553+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-21 22:28:20.56+00</td>
		</tr>
	</table>

7. Enter region - Works ✅

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-enter-foreground</td>
			<td>app will enter foreground</td>
			<td>2017-02-21 22:30:34.711+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-become-active</td>
			<td>app did become active</td>
			<td>2017-02-21 22:30:35.094+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=10.2.1, systemUpTime=211788.715556875, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
			<td>2017-02-21 22:30:35.119+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>did-enter-region</td>
			<td>did enter region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:30:35.169+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-21 22:30:35.188+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-21 22:30:35.192+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x17ea4bb0> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=9.3.4, systemUpTime=7193.94011208333, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
			<td>2017-02-21 22:30:36.414+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>did-enter-region</td>
			<td>did enter region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x17e75020> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:30:36.445+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-21 22:30:36.458+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-21 22:30:36.462+00</td>
		</tr>
	</table>

8. Exit region - Works ✅

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-resign-active</td>
			<td>app will resign active</td>
			<td>2017-02-21 22:32:39.597+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-enter-background</td>
			<td>app did enter background</td>
			<td>2017-02-21 22:32:40.275+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=10.2.1, systemUpTime=211944.158563875, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
			<td>2017-02-21 22:33:10.556+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>did-exit-region</td>
			<td>did exit region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:33:10.604+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-21 22:33:10.617+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-21 22:33:10.632+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x16580b60> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=9.3.4, systemUpTime=7259.659270375, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
			<td>2017-02-21 22:33:33.294+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>did-exit-region</td>
			<td>did exit region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x16554ce0> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:33:33.313+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-21 22:33:33.327+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-21 22:33:33.338+00</td>
		</tr>
	</table>

9. Enter region - Works ✅

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-enter-foreground</td>
			<td>app will enter foreground</td>
			<td>2017-02-21 22:35:44.686+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-become-active</td>
			<td>app did become active</td>
			<td>2017-02-21 22:35:45.088+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=10.2.1, systemUpTime=212077.977623333, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
			<td>2017-02-21 22:35:45.1+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>did-enter-region</td>
			<td>did enter region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:35:45.136+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-21 22:35:45.161+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-21 22:35:45.167+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x16e63340> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=9.3.4, systemUpTime=7293.80453558333, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
			<td>2017-02-21 22:35:46.379+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>did-enter-region</td>
			<td>did enter region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x16d10400> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:35:46.497+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-21 22:35:46.506+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-21 22:35:46.509+00</td>
		</tr>
	</table>

10. Exit region - Works ✅

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-resign-active</td>
			<td>app will resign active</td>
			<td>2017-02-21 22:37:02.378+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-enter-background</td>
			<td>app did enter background</td>
			<td>2017-02-21 22:37:03.056+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=10.2.1, systemUpTime=212186.344917458, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
			<td>2017-02-21 22:37:33.436+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>did-exit-region</td>
			<td>did exit region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:37:33.501+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-21 22:37:33.509+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-21 22:37:33.513+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x16567e90> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=9.3.4, systemUpTime=7332.613824375, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
			<td>2017-02-21 22:37:42.348+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-21 22:37:42.365+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>did-exit-region</td>
			<td>did exit region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x1658f680> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-21 22:37:42.845+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-21 22:37:42.861+00</td>
		</tr>
	</table>


### Display off after rebooting

In this testing scenario, we basically turn off the device, then turn it on and unlock it. Put it into sleep mode. Then stop and start iBeacon signal. 

1. Enter region - Doesn't works ❌

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-enter-foreground</td>
			<td>app will enter foreground</td>
			<td>2017-02-21 22:51:13.175+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-become-active</td>
			<td>app did become active</td>
			<td>2017-02-21 22:51:13.564+00</td>
		</tr>
	</table>

	Note: after 30 minutes, still not seeing any events from both devices.

2. Exit region - Doesn't works ❌

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-resign-active</td>
			<td>app will resign active</td>
			<td>2017-02-21 23:30:34.453+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-enter-background</td>
			<td>app did enter background</td>
			<td>2017-02-21 23:30:35.137+00</td>
		</tr>
	</table>

	Note: after 30 minutes, still not seeing any events from both devices.

3. Enter region - Doesn't works ❌

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-enter-foreground</td>
			<td>app will enter foreground</td>
			<td>2017-02-22 00:05:08.846+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-become-active</td>
			<td>app did become active</td>
			<td>2017-02-22 00:05:09.254+00</td>
		</tr>
	</table>


	looks like rebooting is not working anyway, so we don't wait too long for this case since then. And interestinly, even if we luanch the app manually after rebooting and signal broadcasting, we still don't see any events
	
	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>2</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=10.2.1, systemUpTime=176.877442208333, options=nil</td>
			<td>2017-02-22 00:06:57.821+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>app-did-become-active</td>
			<td>app did become active</td>
			<td>2017-02-22 00:06:57.828+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-22 00:06:57.829+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-22 00:06:57.83+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x14660f20> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=9.3.4, systemUpTime=151.387978458333, options=nil</td>
			<td>2017-02-22 00:07:08.118+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>app-did-become-active</td>
			<td>app did become active</td>
			<td>2017-02-22 00:07:08.143+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-22 00:07:08.17+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-22 00:07:08.174+00</td>
		</tr>
	</table>
	
	And if you stop broadcasting, you can see exit region event without a problem.

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-resign-active</td>
			<td>app will resign active</td>
			<td>2017-02-22 00:08:39.958+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-enter-background</td>
			<td>app did enter background</td>
			<td>2017-02-22 00:08:40.641+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>app-will-resign-active</td>
			<td>app will resign active</td>
			<td>2017-02-22 00:09:00.06+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>app-did-enter-background</td>
			<td>app did enter background</td>
			<td>2017-02-22 00:09:00.065+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>app-will-resign-active</td>
			<td>app will resign active</td>
			<td>2017-02-22 00:09:11.21+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>app-did-enter-background</td>
			<td>app did enter background</td>
			<td>2017-02-22 00:09:11.219+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>did-exit-region</td>
			<td>did exit region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x14622b90> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-22 00:09:14.952+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>did-exit-region</td>
			<td>did exit region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-22 00:11:05.786+00</td>
		</tr>
	</table>
	
	So our guess, the OS is working fine managing the state of iBeacon regions, however, previous registrations for region monitoring from apps are not persisted or not present after reboot.

4. Exit region - Doesn't works ❌

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-resign-active</td>
			<td>app will resign active</td>
			<td>2017-02-22 00:38:01.221+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-enter-background</td>
			<td>app did enter background</td>
			<td>2017-02-22 00:38:01.896+00</td>
		</tr>
	</table>
	
	And like what we saw with previous entering region test, even if we start the app manually after stop broadcasting, we won't see the exit region event.

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>2</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=10.2.1, systemUpTime=194.661072333333, options=nil</td>
			<td>2017-02-22 00:41:02.665+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>app-did-become-active</td>
			<td>app did become active</td>
			<td>2017-02-22 00:41:02.673+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-22 00:41:02.674+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-22 00:41:02.675+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>app-launch</td>
			<td>app launched, monitoring CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x165b78f0> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1), os_version=9.3.4, systemUpTime=176.655739416667, options=nil</td>
			<td>2017-02-22 00:41:05.831+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>app-did-become-active</td>
			<td>app did become active</td>
			<td>2017-02-22 00:41:05.879+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cb-power-on</td>
			<td>CoreBluetooth power on</td>
			<td>2017-02-22 00:41:05.887+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>cl-authorized-always</td>
			<td>CoreLocation authorized always</td>
			<td>2017-02-22 00:41:05.895+00</td>
		</tr>
	</table>

	However, if we start broadcasting again, we can see the enter event after we manually launch the app. 

	<table>
		<tr>
			<th>user_id</th>
			<th>event</th>
			<th>message</th>
			<th>created_at</th>
		</tr>
		<tr>
			<td>1</td>
			<td>app-will-enter-foreground</td>
			<td>app will enter foreground</td>
			<td>2017-02-22 00:43:15.532+00</td>
		</tr>
		<tr>
			<td>3</td>
			<td>did-enter-region</td>
			<td>did enter region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:&lt;__NSConcreteUUID 0x165800b0> 5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-22 00:43:15.653+00</td>
		</tr>
		<tr>
			<td>1</td>
			<td>app-did-become-active</td>
			<td>app did become active</td>
			<td>2017-02-22 00:43:15.96+00</td>
		</tr>
		<tr>
			<td>2</td>
			<td>did-enter-region</td>
			<td>did enter region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
			<td>2017-02-22 00:43:16.036+00</td>
		</tr>
	</table>


## Daily sign-in tests

TODO:
