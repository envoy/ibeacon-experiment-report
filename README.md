# iBeacon not working with iPhone issue investigation report

## Manual testing with scenarios

User 1 is the iPad app, and user 2 is the iPhone app.

### Display off

iPhone status:
 - Unplugged

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
		<td>2017-02-18 00:11:02.171+00</td>
	</tr>
	<tr>
		<td>1</td>
		<td>app-did-become-active</td>
		<td>app did become active</td>
		<td>2017-02-18 00:11:02.553+00</td>
	</tr>
	<tr>
		<td>2</td>
		<td>did-enter-region</td>
		<td>did enter region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
		<td>2017-02-18 00:11:03.83+00</td>
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
		<td>2017-02-18 00:13:52.27+00</td>
	</tr>
	<tr>
		<td>1</td>
		<td>app-did-enter-background</td>
		<td>app did enter background</td>
		<td>2017-02-18 00:13:52.946+00</td>
	</tr>
	<tr>
		<td>2</td>
		<td>did-exit-region</td>
		<td>did exit region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
		<td>2017-02-18 00:14:26.119+00</td>
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
		<td>2017-02-18 00:18:27.805+00</td>
	</tr>
	<tr>
		<td>1</td>
		<td>app-did-become-active</td>
		<td>app did become active</td>
		<td>2017-02-18 00:18:28.198+00</td>
	</tr>
	<tr>
		<td>2</td>
		<td>did-enter-region</td>
		<td>did enter region CLBeaconRegion (identifier:'ibeacon-test.envoy.com', uuid:5E759524-B7F2-4F3A-81E6-73B2F9728AAB, major:1, minor:1)</td>
		<td>2017-02-18 00:18:28.962+00</td>
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
