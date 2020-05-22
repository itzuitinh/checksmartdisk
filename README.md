Hướng dẫn cấu hình check S.M.A.R.T disk Centron
===========
Cài các gói cần thiết
-------------------------
    sudo apt install nagios-nrpe-server nagios-plugins smartmontools
Chỉnh sửa sudoers
    nagios   ALL = NOPASSWD: /usr/lib/nagios/plugins/check_smart.pl    # for option 1
    nagios   ALL = NOPASSWD: /usr/local/sbin/smartctl                  # for option 2
    
Cấu hình cho nrpe
-------------------------
    vi /etc/nagios/nrpe.cfg 
    allowed_hosts=127.0.0.1, 103.70.30.229, 10.0.2.250
    dont_blame_nrpe=1
    command[check_smart]=sudo /usr/lib/nagios/plugins/check_smart.pl -d $ARG1$ -i auto -w 'Current_Pending_Sector=14,Reallocated_Sector_Count=3'
	/etc/init.d/nagios-nrpe-server restart
	systemctl enable nagios-nrpe-server.service
Tải về script check _mart.pl
-------------------------
    cd /usr/lib/nagios/plugins/
    wget https://www.claudiokuenzler.com/monitoring-plugins/check_smart.pl
    chmod +x check_smart.pl

