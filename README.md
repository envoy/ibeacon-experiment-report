# iBeacon not working with iPhone issue investigation report

## Manual scenario tests

### Display off

iPhone status:
 - Unplugged

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

### Display off + App killed

### Display off after rebooting

TODO:

1. Enter
2. Exit
3. Enter and exit

## Daily sign-in tests

TODO:
