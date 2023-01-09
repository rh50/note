
# timedatectl

## timedatectl
	timedatectl
		查看时间各种状态：
	timedatectl list-timezones
		列出所有时区
	timedatectl set-local-rtc 1
		将硬件时钟调整为与本地时钟一致, 0 为设置为 UTC 时间
	timedatectl set-timezone Asia/Shanghai
		设置系统时区为上海

## 校准时间
	yum -y install ntp
	# 通过阿里云时间服务器校准时间
	ntpdate ntp1.aliyun.com
