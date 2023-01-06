
## 带日期重定向日志

00 11 * * * /root/exe.sh >> "/var/log/exe-$(date +"\%Y-\%m-\%d").log" 2>&1

00 11 * * * /root/exe.sh >> /var/log/exe-$(date +""\%Y-\%m-\%d"").log
