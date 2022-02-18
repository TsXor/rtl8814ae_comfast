# rtl8814ae_comfast
I got a linux driver for rtl8814ae_comfast, but it only support up to kernel version 4.4, so I managed to extinguish all the make errors, but after being inserted the module just does not work and I got no wireless interface.  
Now I upload it to github, hoping to get some assist.

# commits I made
Here are the commits I made to let it successfully complie.
<table class="tg">
<thead>
  <tr>
    <th class="tg-0pky">Error</th>
    <th class="tg-0pky">On kernel above</th>
    <th class="tg-0pky">Solution</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky">timer</td>
    <td class="tg-0pky">4.15</td>
    <td class="tg-0pky"><a href="https://github.com/aircrack-ng/rtl8812au/commit/f221a169f281dab9756a176ec2abd91e0eba7d19">link</a></td>
  </tr>
  <tr>
    <td class="tg-0pky">sha256</td>
    <td class="tg-0pky">5.8</td>
    <td class="tg-0pky"><a href="https://github.com/aircrack-ng/rtl8188eus/pull/77/files">link</a></td>
  </tr>
  <tr>
    <td class="tg-0pky">set/get_fs</td>
    <td class="tg-0pky">Unknown</td>
    <td class="tg-0pky"><a href="https://github.com/jwrdegoede/rtl8189ES_linux/pull/50/files">link1</a>; <a href="https://github.com/aircrack-ng/rtl8812au/commit/4573749621508b6799b84e92d6b08505fc5a2a7e">link2</a>(*also in rtw_efuse.c)</td>
  </tr>
  <tr>
    <td class="tg-0pky">vfs_read/write</td>
	<td class="tg-0pky">4.14</td>
	<td class="tg-0pky"><a href="https://github.com/chenhaiq/mt7610u_wifi_sta_v3002_dpo_20130916/issues/43">link1</a>; <a href="https://github.com/zebulon2/rtl8812au-driver-5.2.9/commit/08e0472fbc60be09f6207b21819ed141cb81d579">link2</a>(*also in rtw_efuse.c)</td>
  </tr>
  <tr>
    <td class="tg-0pky">rtw_select_queue</td>
	<td class="tg-0pky">5.2 & 4.19</td>
	<td class="tg-0pky"><a href="https://github.com/maccuaa/asus-ac53-rtl8822bu/commit/5b8a9c1bffb621236c6b3e7423b37841722fa4f8">link</a></td>
  </tr>
  <tr>
    <td class="tg-0pky">date&time(warning)</td>
	<td class="tg-0pky">N/A</td>
	<td class="tg-0pky"><a href="https://github.com/RinCat/RTL88x2BU-Linux-Driver/issues/100">link</a></td>
  </tr>
  <tr>
    <td class="tg-0pky">IEEE80211_MAX_AMPDU_BUF redefine(warning)</td>
	<td class="tg-0pky">4.19</td>
	<td class="tg-0pky"><a href="https://github.com/clnhub/rtl8192eu-linux/commit/2628f6dfd941357fcefeb4e2adcf9855a2440e5c">link</a></td>
  </tr>
  <tr>
    <td class="tg-0pky">is_compat_task</td>
	<td class="tg-0pky">4.6</td>
	<td class="tg-0pky"><a href="https://github.com/ivanovborislav/rtl8188eu/blob/main/os_dep/linux/ioctl_linux.c">link</a>(modified according to codes near is_compat_task)<br>(*also in rtw_android.c)</td>
  </tr>
  <tr>
    <td class="tg-0pky">IEEE80211_band</td>
	<td class="tg-0pky">4.7</td>
	<td class="tg-0pky"><a href="https://github.com/diederikdehaas/rtl8812AU/commit/01404a0ce3b4602e7eab1672a251f2bf16cce503">link</a></td>
  </tr>
  <tr>
    <td class="tg-0pky">cfg80211_roamed incompatible pointer type</td>
	<td class="tg-0pky">4.12</td>
	<td class="tg-0pky"><a href="https://github.com/mk-fg/rtl8812au/commit/974f7a8a29e18580c8f0daaa931728d23a627e3f">link</a></td>
  </tr>
  <tr>
    <td class="tg-0pky">get_monotonic_boottime (get_boottime in some drivers)</td>
	<td class="tg-0pky">4.20</td>
	<td class="tg-0pky"><a href="https://github.com/smlinux/rtl8723de/pull/33/files">link</a>(This commit raises new error, and I had to change `ktime_to_timespec` to `ktime_to_timespec64`)<br><a href="https://github.com/ivanovborislav/rtl8188eu/blob/main/os_dep/linux/ioctl_cfg80211.c">link</a>(found modifying according to codes near `get_monotonic_boottime(&ts)` better, and also solved the "ts unknown" error)</td>
  </tr>
  <tr>
    <td class="tg-0pky">‘struct cfg80211_scan_info *’ type ‘bool’</td>
	<td class="tg-0pky">4.8</td>
	<td class="tg-0pky"><a href="https://github.com/abperiasamy/rtl8812AU_8821AU_linux/pull/148/files">link</a>(The <a href="https://github.com/abperiasamy/rtl8812AU_8821AU_linux/pull/143/files">first attempt</a> was <a href="https://github.com/abperiasamy/rtl8812AU_8821AU_linux/pull/147">reverted</a>)</td>
  </tr>
  <tr>
    <td class="tg-0pky">destructor</td>
	<td class="tg-0pky">4.12</td>
	<td class="tg-0pky"><a href="https://github.com/FomalhautWeisszwerg/rtl8822bu/commit/49821e5beee8e424ac00ae8c5a9725554ca7287e">link</a></td>
  </tr>
  <tr>
    <td class="tg-0pky">access_ok</td>
	<td class="tg-0pky">5.0</td>
	<td class="tg-0pky"><a href="https://github.com/Mange/rtl8192eu-linux-driver/pull/110/files">link</a></td>
  </tr>
  <tr>
    <td class="tg-0pky">proc_create_data incompatible pointer type</td>
	<td class="tg-0pky">5.6</td>
	<td class="tg-0pky"><a href="https://github.com/tomaspinho/rtl8821ce/pull/126/files">link</a>(my driver only have functions called `rtw_drv_*_fops` using `single_release`)</td>
  </tr>
  <tr>
    <td class="tg-0pky">ISO C90 forbids variable length array ‘input’(warning)</td>
	<td class="tg-0pky">N/A</td>
	<td class="tg-0pky"><a href="https://github.com/jmfernandezidealista/rtl8812au/commit/2eb86a834977f56c82a0079b0a2c8302f5ab7501">link</a></td>
  </tr>
  <tr>
    <td class="tg-0pky">‘struct net_device’ has no member named ‘trans_start’</td>
	<td class="tg-0pky">4.7</td>
	<td class="tg-0pky"><a href="https://github.com/yinkangning0124/RTL8821ce-for-ubuntu/blob/2db2c6ded7cc03c8d25896100909bf9401ad4ec3/hal/rtl8821c/pci/rtl8821ce_io.c">link</a>(modified according to codes near `padapter->pnetdev->trans_start = jiffies;`)</td>
  </tr>
</tbody>
</table>
