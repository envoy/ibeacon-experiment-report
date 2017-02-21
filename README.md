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


### Display off + App killed

### Display off after rebooting

TODO:

1. Enter
2. Exit
3. Enter and exit

## Daily sign-in tests

TODO:
