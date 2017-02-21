# iBeacon not working with iPhone issue investigation report

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

### Display off after rebooting

TODO:

1. Enter
2. Exit
3. Enter and exit

## Daily sign-in tests

TODO:
