## 1. enter (working)

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
		<td>2017-04-06 18:03:05.365+00</td>
	</tr>
	<tr>
		<td>1</td>
		<td>app-did-become-active</td>
		<td>app did become active</td>
		<td>2017-04-06 18:03:05.782+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>app-launch</td>
		<td>app launched, monitoring CLBeaconRegion (identifier:'manual-ibeacon-test.envoy.com', uuid:EAD09230-2176-4ABD-85A0-A54A8EB343B1, major:1, minor:1), os_version=10.3.1, systemUpTime=331.199760583333, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
		<td>2017-04-06 18:03:06.299+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>did-enter-region</td>
		<td>did enter region CLBeaconRegion (identifier:'manual-ibeacon-test.envoy.com', uuid:EAD09230-2176-4ABD-85A0-A54A8EB343B1, major:1, minor:1)</td>
		<td>2017-04-06 18:03:06.304+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>cb-power-on</td>
		<td>CoreBluetooth power on</td>
		<td>2017-04-06 18:03:06.306+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>cl-authorized-always</td>
		<td>CoreLocation authorized always</td>
		<td>2017-04-06 18:03:06.307+00</td>
	</tr>
</table>

## 2. exit working

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
		<td>2017-04-06 18:11:50.021+00</td>
	</tr>
	<tr>
		<td>1</td>
		<td>app-did-enter-background</td>
		<td>app did enter background</td>
		<td>2017-04-06 18:11:50.491+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>app-launch</td>
		<td>app launched, monitoring CLBeaconRegion (identifier:'manual-ibeacon-test.envoy.com', uuid:EAD09230-2176-4ABD-85A0-A54A8EB343B1, major:1, minor:1), os_version=10.3.1, systemUpTime=462.199299583333, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
		<td>2017-04-06 18:12:21.7+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>did-exit-region</td>
		<td>did exit region CLBeaconRegion (identifier:'manual-ibeacon-test.envoy.com', uuid:EAD09230-2176-4ABD-85A0-A54A8EB343B1, major:1, minor:1)</td>
		<td>2017-04-06 18:12:21.717+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>cb-power-on</td>
		<td>CoreBluetooth power on</td>
		<td>2017-04-06 18:12:21.72+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>cl-authorized-always</td>
		<td>CoreLocation authorized always</td>
		<td>2017-04-06 18:12:21.721+00</td>
	</tr>
</table>

## 3. enter (not working)

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
		<td>2017-04-06 18:20:40.326+00</td>
	</tr>
	<tr>
		<td>1</td>
		<td>app-did-become-active</td>
		<td>app did become active</td>
		<td>2017-04-06 18:20:40.729+00</td>
	</tr>
</table>

TODO: maybe somehow iPhone thinks it's still in the region, maybe try to switch broadcasting on and off next time.

## 4. exit working

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
		<td>2017-04-06 18:35:36.687+00</td>
	</tr>
	<tr>
		<td>1</td>
		<td>app-did-enter-background</td>
		<td>app did enter background</td>
		<td>2017-04-06 18:35:37.191+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>app-launch</td>
		<td>app launched, monitoring CLBeaconRegion (identifier:'manual-ibeacon-test.envoy.com', uuid:EAD09230-2176-4ABD-85A0-A54A8EB343B1, major:1, minor:1), os_version=10.3.1, systemUpTime=244.689974625, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
		<td>2017-04-06 18:36:08.52+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>did-exit-region</td>
		<td>did exit region CLBeaconRegion (identifier:'manual-ibeacon-test.envoy.com', uuid:EAD09230-2176-4ABD-85A0-A54A8EB343B1, major:1, minor:1)</td>
		<td>2017-04-06 18:36:08.538+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>cb-power-on</td>
		<td>CoreBluetooth power on</td>
		<td>2017-04-06 18:36:08.541+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>cl-authorized-always</td>
		<td>CoreLocation authorized always</td>
		<td>2017-04-06 18:36:08.543+00</td>
	</tr>
</table>

## 5. enter not working

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
		<td>2017-04-06 18:44:10.346+00</td>
	</tr>
	<tr>
		<td>1</td>
		<td>app-did-become-active</td>
		<td>app did become active</td>
		<td>2017-04-06 18:44:10.756+00</td>
	</tr>
</table>


but, my bet is somehow iPhone is confused, maybe it thinks it's in the region, so I put the iBeacon advertising app to background, and it does receive exit region event

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
		<td>2017-04-06 18:46:41.571+00</td>
	</tr>
	<tr>
		<td>1</td>
		<td>app-did-enter-background</td>
		<td>app did enter background</td>
		<td>2017-04-06 18:46:42.097+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>app-launch</td>
		<td>app launched, monitoring CLBeaconRegion (identifier:'manual-ibeacon-test.envoy.com', uuid:EAD09230-2176-4ABD-85A0-A54A8EB343B1, major:1, minor:1), os_version=10.3.1, systemUpTime=344.387114166667, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
		<td>2017-04-06 18:47:16.209+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>did-exit-region</td>
		<td>did exit region CLBeaconRegion (identifier:'manual-ibeacon-test.envoy.com', uuid:EAD09230-2176-4ABD-85A0-A54A8EB343B1, major:1, minor:1)</td>
		<td>2017-04-06 18:47:16.215+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>cb-power-on</td>
		<td>CoreBluetooth power on</td>
		<td>2017-04-06 18:47:16.216+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>cl-authorized-always</td>
		<td>CoreLocation authorized always</td>
		<td>2017-04-06 18:47:16.217+00</td>
	</tr>
</table>

## 6. exit working

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
		<td>2017-04-06 18:58:48.916+00</td>
	</tr>
	<tr>
		<td>1</td>
		<td>app-did-enter-background</td>
		<td>app did enter background</td>
		<td>2017-04-06 18:58:49.424+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>app-launch</td>
		<td>app launched, monitoring CLBeaconRegion (identifier:'manual-ibeacon-test.envoy.com', uuid:EAD09230-2176-4ABD-85A0-A54A8EB343B1, major:1, minor:1), os_version=10.3.1, systemUpTime=266.502404166667, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
		<td>2017-04-06 18:59:22.701+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>did-exit-region</td>
		<td>did exit region CLBeaconRegion (identifier:'manual-ibeacon-test.envoy.com', uuid:EAD09230-2176-4ABD-85A0-A54A8EB343B1, major:1, minor:1)</td>
		<td>2017-04-06 18:59:22.717+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>cl-authorized-always</td>
		<td>CoreLocation authorized always</td>
		<td>2017-04-06 18:59:22.72+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>cb-power-on</td>
		<td>CoreBluetooth power on</td>
		<td>2017-04-06 18:59:22.722+00</td>
	</tr>
</table>

## 7. enter working

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
		<td>2017-04-06 19:08:28.983+00</td>
	</tr>
	<tr>
		<td>1</td>
		<td>app-did-become-active</td>
		<td>app did become active</td>
		<td>2017-04-06 19:08:29.388+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>app-launch</td>
		<td>app launched, monitoring CLBeaconRegion (identifier:'manual-ibeacon-test.envoy.com', uuid:EAD09230-2176-4ABD-85A0-A54A8EB343B1, major:1, minor:1), os_version=10.3.1, systemUpTime=293.531426583333, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
		<td>2017-04-06 19:08:32.572+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>did-enter-region</td>
		<td>did enter region CLBeaconRegion (identifier:'manual-ibeacon-test.envoy.com', uuid:EAD09230-2176-4ABD-85A0-A54A8EB343B1, major:1, minor:1)</td>
		<td>2017-04-06 19:08:32.597+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>cl-authorized-always</td>
		<td>CoreLocation authorized always</td>
		<td>2017-04-06 19:08:32.6+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>cb-power-on</td>
		<td>CoreBluetooth power on</td>
		<td>2017-04-06 19:08:32.601+00</td>
	</tr>
</table>

## 8. exit working

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
		<td>2017-04-06 19:20:14.879+00</td>
	</tr>
	<tr>
		<td>1</td>
		<td>app-did-enter-background</td>
		<td>app did enter background</td>
		<td>2017-04-06 19:20:15.386+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>app-launch</td>
		<td>app launched, monitoring CLBeaconRegion (identifier:'manual-ibeacon-test.envoy.com', uuid:EAD09230-2176-4ABD-85A0-A54A8EB343B1, major:1, minor:1), os_version=10.3.1, systemUpTime=444.212863125, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
		<td>2017-04-06 19:20:47.798+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>did-exit-region</td>
		<td>did exit region CLBeaconRegion (identifier:'manual-ibeacon-test.envoy.com', uuid:EAD09230-2176-4ABD-85A0-A54A8EB343B1, major:1, minor:1)</td>
		<td>2017-04-06 19:20:47.805+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>cb-power-on</td>
		<td>CoreBluetooth power on</td>
		<td>2017-04-06 19:20:47.806+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>cl-authorized-always</td>
		<td>CoreLocation authorized always</td>
		<td>2017-04-06 19:20:47.807+00</td>
	</tr>
</table>

## 9. enter working

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
		<td>2017-04-06 19:30:23.179+00</td>
	</tr>
	<tr>
		<td>1</td>
		<td>app-did-become-active</td>
		<td>app did become active</td>
		<td>2017-04-06 19:30:23.583+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>app-launch</td>
		<td>app launched, monitoring CLBeaconRegion (identifier:'manual-ibeacon-test.envoy.com', uuid:EAD09230-2176-4ABD-85A0-A54A8EB343B1, major:1, minor:1), os_version=10.3.1, systemUpTime=337.432874291667, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
		<td>2017-04-06 19:30:24.876+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>did-enter-region</td>
		<td>did enter region CLBeaconRegion (identifier:'manual-ibeacon-test.envoy.com', uuid:EAD09230-2176-4ABD-85A0-A54A8EB343B1, major:1, minor:1)</td>
		<td>2017-04-06 19:30:24.904+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>cl-authorized-always</td>
		<td>CoreLocation authorized always</td>
		<td>2017-04-06 19:30:24.906+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>cb-power-on</td>
		<td>CoreBluetooth power on</td>
		<td>2017-04-06 19:30:24.911+00</td>
	</tr>
</table>

## 10. exiting working

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
		<td>2017-04-06 19:47:45.568+00</td>
	</tr>
	<tr>
		<td>1</td>
		<td>app-did-enter-background</td>
		<td>app did enter background</td>
		<td>2017-04-06 19:47:46.045+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>app-launch</td>
		<td>app launched, monitoring CLBeaconRegion (identifier:'manual-ibeacon-test.envoy.com', uuid:EAD09230-2176-4ABD-85A0-A54A8EB343B1, major:1, minor:1), os_version=10.3.1, systemUpTime=415.16216425, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
		<td>2017-04-06 19:48:20.511+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>did-exit-region</td>
		<td>did exit region CLBeaconRegion (identifier:'manual-ibeacon-test.envoy.com', uuid:EAD09230-2176-4ABD-85A0-A54A8EB343B1, major:1, minor:1)</td>
		<td>2017-04-06 19:48:20.518+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>cb-power-on</td>
		<td>CoreBluetooth power on</td>
		<td>2017-04-06 19:48:20.52+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>cl-authorized-always</td>
		<td>CoreLocation authorized always</td>
		<td>2017-04-06 19:48:20.521+00</td>
	</tr>
</table>

## 11. enter working

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
		<td>2017-04-06 20:02:42.438+00</td>
	</tr>
	<tr>
		<td>1</td>
		<td>app-did-become-active</td>
		<td>app did become active</td>
		<td>2017-04-06 20:02:42.835+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>app-launch</td>
		<td>app launched, monitoring CLBeaconRegion (identifier:'manual-ibeacon-test.envoy.com', uuid:EAD09230-2176-4ABD-85A0-A54A8EB343B1, major:1, minor:1), os_version=10.3.1, systemUpTime=326.008358125, options=Optional([__C.UIApplicationLaunchOptionsKey(_rawValue: UIApplicationLaunchOptionsLocationKey): 1])</td>
		<td>2017-04-06 20:02:44.095+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>did-enter-region</td>
		<td>did enter region CLBeaconRegion (identifier:'manual-ibeacon-test.envoy.com', uuid:EAD09230-2176-4ABD-85A0-A54A8EB343B1, major:1, minor:1)</td>
		<td>2017-04-06 20:02:44.108+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>cl-authorized-always</td>
		<td>CoreLocation authorized always</td>
		<td>2017-04-06 20:02:44.114+00</td>
	</tr>
	<tr>
		<td>5</td>
		<td>cb-power-on</td>
		<td>CoreBluetooth power on</td>
		<td>2017-04-06 20:02:44.122+00</td>
	</tr>
</table>

