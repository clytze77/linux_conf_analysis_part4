#Linux4.0.4 配置文件解析
###P14206034 高齐琦   
 * [1.配置解析](#1)
 * [2.实验中遇到的问题及解决办法](#2)
 
这篇文档介绍的是编译[Linux4.0.4][1]源码时的部分配置文件的说明文档,参考的配置文件[myconfig2][2]的第四部分，该配置条件下可保证完成内核的上网功能。主要包含I2C协议的配置，图形方面的配置和时钟源驱动的配置等。
<h1 id="1">配置解析</h1>
##Serial drivers的配置
    Serial drivers
    
    CONFIG_SERIAL_8250=y
    #8250芯片串口驱动配置
    CONFIG_SERIAL_8250_DEPRECATED_OPTIONS=y
    CONFIG_SERIAL_8250_CONSOLE is not set
    CONFIG_SERIAL_8250_PCI=y
    CONFIG_SERIAL_8250_NR_UARTS=4
    CONFIG_SERIAL_8250_RUNTIME_UARTS=4
    #linux发行的8250驱动一般默认限制检测的最大串口数量是4，
    #配置项RUNTIME_UARTS限制了这个数目，但如果安装了16个串口
    #的串口卡来扩充机器的窗口数目，那么只能得到4个，解决的
    #方法可以是重新配置内核并编译，但更方便的方法是通过内
    #核启动参数8250_NR_UARTS=？？来改变默认数。
    
    CONFIG_SERIAL_8250_EXTENDED is not set
    CONFIG_SERIAL_8250_DW is not set
##serial port support的配置 
    
     Non-8250 serial port support 
    #支持对非8250串口驱动设备
    CONFIG_SERIAL_MFD_HSU is not set
    CONFIG_SERIAL_CORE=y 
    #仅仅配置串口内核，其他的串口设备不给予支持
    CONFIG_SERIAL_JSM is not set
    CONFIG_SERIAL_SCCNXP is not set
    CONFIG_SERIAL_TIMBERDALE is not set
    CONFIG_SERIAL_ALTERA_JTAGUART is not set
    CONFIG_SERIAL_ALTERA_UART is not set
    CONFIG_SERIAL_PCH_UART is not set
    CONFIG_SERIAL_ARC is not set
    CONFIG_SERIAL_RP2 is not set
    CONFIG_SERIAL_FSL_LPUART is not set
    CONFIG_TTY_PRINTK is not set
    CONFIG_IPMI_HANDLER is not set
    CONFIG_HW_RANDOM is not set
    CONFIG_NVRAM is not set
    CONFIG_R3964 is not set
    CONFIG_APPLICOM is not set
    CONFIG_SONYPI is not set
    CONFIG_MWAVE is not set
    CONFIG_PC8736x_GPIO is not set
    CONFIG_NSC_GPIO is not set
    CONFIG_HANGCHECK_TIMER is not set
    CONFIG_TCG_TPM is not set
    CONFIG_TELCLOCK is not set
    CONFIG_DEVPORT=y
    CONFIG_XILLYBUS is not set
##I2C support的配置
    
    I2C support
    #用于感知硬件状态，比如温度，风扇转速。
    I2C是Philips极力推动的微控制应用中使用的低速串行总线协议。
    如果要支持Video For Linux，该项必选。这里不配置
    CONFIG_I2C is not set
    CONFIG_SPI is not set
    CONFIG_SPMI is not set
    CONFIG_HSI is not set
    
    
    PPS support 
    CONFIG_PPS=y
    #开发对PPS的支持
    CONFIG_PPS_DEBUG is not set
    #PPS调试功能
    CONFIG_NTP_PPS is not set
    
    
    PPS clients support
    #PPS客户端支持
    CONFIG_PPS_CLIENT_KTIMER is not set
    CONFIG_PPS_CLIENT_LDISC is not set
    CONFIG_PPS_CLIENT_GPIO is not set
    
   
    PPS generators support
    
##PTP clock support的配置  
    
    PTP clock support
    
    CONFIG_PTP_1588_CLOCK=y
    --PTP（Precision Time Protocol，精确时间协议）是一个时间同步的协议，1588是网络测量和控制
    系统的精密时钟同步协议标准，采用PTP协议，这里的配置PTP时钟，是为了网络通信中，保持设备的时间和频率同步。
    
    Enable PHYLIB and NETWORK_PHY_TIMESTAMPING to see the additional clocks.
    
    CONFIG_PTP_1588_CLOCK_PCH is not set
    CONFIG_ARCH_WANT_OPTIONAL_GPIOLIB=y 
    --使用gpiolib并把它编译进内核。GPIO（“通用目的输入/输出端口”）是一个灵活的软件控制的数字信号，用于控制输入输出。
    CONFIG_GPIOLIB is not set
    CONFIG_W1 is not set
    CONFIG_POWER_SUPPLY is not set
    CONFIG_POWER_AVS is not set
    CONFIG_HWMON is not set
    CONFIG_THERMAL is not set
    CONFIG_WATCHDOG is not set
    CONFIG_SSB_POSSIBLE=y --？？？？
##Sonics Silicon Backplane的配置    
    
    # Sonics Silicon Backplane
    
    CONFIG_SSB is not set
    CONFIG_BCMA_POSSIBLE=y --？？
    
    
    Broadcom specific AMBA
    
    CONFIG_BCMA is not set
    
    
    Multifunction device drivers --不使用多功能设备
    
     CONFIG_MFD_CORE is not set
     CONFIG_MFD_CS5535 is not set
     CONFIG_MFD_CROS_EC is not set
     CONFIG_HTC_PASIC3 is not set
     CONFIG_LPC_ICH is not set
     CONFIG_LPC_SCH is not set
     CONFIG_MFD_JANZ_CMODIO is not set
     CONFIG_MFD_KEMPLD is not set
     CONFIG_MFD_RDC321X is not set
     CONFIG_MFD_RTSX_PCI is not set
     CONFIG_MFD_SM501 is not set
     CONFIG_ABX500_CORE is not set
     CONFIG_MFD_SYSCON is not set
     CONFIG_MFD_TI_AM335X_TSCADC is not set
     CONFIG_MFD_TMIO is not set
     CONFIG_MFD_VX855 is not set
     CONFIG_REGULATOR is not set
     CONFIG_MEDIA_SUPPORT is not set
##Graphics support 的配置    
    
    Graphics support --图形支持，支持VGA接口，最多使用的GPU为16
    
    CONFIG_AGP is not set
    CONFIG_VGA_ARB=y
    CONFIG_VGA_ARB_MAX_GPUS=16
    
    
    Direct Rendering Manager
    
    CONFIG_DRM is not set
    
    
    Frame buffer Devices
    #帧缓冲器设备
    CONFIG_FB is not set
    CONFIG_BACKLIGHT_LCD_SUPPORT is not set 灯背后照片设置，不需要
    CONFIG_VGASTATE is not set 显示状态不需要配置
    
    
    Console display driver support
    
    CONFIG_VGA_CONSOLE=y
    CONFIG_VGACON_SOFT_SCROLLBACK is not set
    CONFIG_DUMMY_CONSOLE=y --控制台演示驱动，设置虚拟演示台的宽度与长度分别为80和25.
    CONFIG_DUMMY_CONSOLE_COLUMNS=80
    CONFIG_DUMMY_CONSOLE_ROWS=25
    CONFIG_SOUND is not set
##HID support的配置    
    
    
    HID support
    #人力工程学设备，不需要
    CONFIG_HID is not set
    CONFIG_USB_OHCI_LITTLE_ENDIAN=y
    注册开放型USB主机控制器驱动
     CONFIG_USB_SUPPORT is not set
     CONFIG_UWB is not set
     CONFIG_MMC is not set
     CONFIG_MEMSTICK is not set
     CONFIG_NEW_LEDS is not set
     CONFIG_ACCESSIBILITY is not set
     CONFIG_INFINIBAND is not set
     CONFIG_EDAC is not set
     CONFIG_RTC_LIB=y --引入函数库，提供一些辅助函数，闰年计算，日期有效性验证之类的。
     CONFIG_RTC_CLASS is not set
     CONFIG_DMADEVICES is not set
     CONFIG_AUXDISPLAY is not set
     CONFIG_UIO is not set
     CONFIG_VIRT_DRIVERS is not set
##virtio网卡配置驱动的配置   
    
     Virtio drivers --virtio网卡配置驱动
    
     CONFIG_VIRTIO_PCI is not set
     CONFIG_VIRTIO_MMIO is not set
    
    
     Microsoft Hyper-V guest support
    
     CONFIG_STAGING is not set
     CONFIG_X86_PLATFORM_DEVICES is not set
     CONFIG_CHROME_PLATFORMS is not set
    
    
     Hardware Spinlock drivers
    
##时钟源驱动配置    
    
     Clock Source drivers --时钟源驱动配置
    
    CONFIG_CLKSRC_I8253=y  --时钟频率
    CONFIG_CLKEVT_I8253=y  --计数时钟clkevt，计数模式时的外部计数脉冲信号。
    CONFIG_CLKBLD_I8253=y
     CONFIG_ATMEL_PIT is not set
     CONFIG_SH_TIMER_CMT is not set
     CONFIG_SH_TIMER_MTU2 is not set
     CONFIG_SH_TIMER_TMU is not set
     CONFIG_EM_TIMER_STI is not set
     CONFIG_MAILBOX is not set
     CONFIG_IOMMU_SUPPORT is not set
    
    
     Remoteproc drivers
    
     CONFIG_STE_MODEM_RPROC is not set
    
    
     Rpmsg drivers
    
##SOC (System On Chip) specific Drivers的配置   
    
     SOC (System On Chip) specific Drivers
    
     CONFIG_SOC_TI is not set
     CONFIG_PM_DEVFREQ is not set
     CONFIG_EXTCON is not set
     CONFIG_MEMORY is not set
     CONFIG_IIO is not set
     CONFIG_NTB is not set
     CONFIG_VME_BUS is not set
     CONFIG_PWM is not set
     CONFIG_IPACK_BUS is not set
     CONFIG_RESET_CONTROLLER is not set
     CONFIG_FMC is not set
##PHY Subsystem的配置     
    
     PHY Subsystem
     PHY ( 物理层控制芯片)
     CONFIG_GENERIC_PHY is not set
     CONFIG_BCM_KONA_USB2_PHY is not set
     CONFIG_POWERCAP is not set
     CONFIG_MCB is not set
     CONFIG_THUNDERBOLT is not set
    
    
     Android
    
     CONFIG_ANDROID is not set
    
    
     Firmware Drivers 固件驱动
    
     CONFIG_EDD is not set
     CONFIG_FIRMWARE_MEMMAP is not set
     CONFIG_DELL_RBU is not set
     CONFIG_DCDBAS is not set
     CONFIG_GOOGLE_FIRMWARE is not set

##File systems的配置    
    
     File systems
    
    CONFIG_DCACHE_WORD_ACCESS=y
    CONFIG_FS_POSIX_ACL is not set
    CONFIG_FILE_LOCKING is not set
    CONFIG_FSNOTIFY is not set
    CONFIG_DNOTIFY is not set 基于目录的文件变化的通知机制
    CONFIG_INOTIFY_USER is not set 用户空间的Inotify支持。（notify 是一个 Linux特性，它监控文件系统操作，比如读取、写入和创建）
    CONFIG_FANOTIFY is not set
    CONFIG_QUOTA is not set
    CONFIG_QUOTACTL is not set
    CONFIG_AUTOFS4_FS is not set
    CONFIG_FUSE_FS is not set ：FUSE（Filesystem in Userspace），允许在用户空间实现一个文件系统，如果打算开发一个自己的文件系统或使用一个机遇FUSE的文件系统，可以打开，这里不设置。
    CONFIG_OVERLAY_FS is not set
    

<h1 id="2">实验中遇到的问题及解决办法</h1>
 [2.实验中遇到的问题及解决办法](#2)
###问题一：make menuconfig curses.h：No such file or directory
#####解决方案：安装ncurses，sudo apt-get install libncurses5-dev

###问题二：预安装的qemu由于版本的问题，命令麻烦
#####问题描述：预安装的qemu使用qemu-system-i386时有时会操作失败
#####解决方案：安装新的qemu，sudo apt-get install qemu

#引用：



[1]:https://www.kernel.org/
[2]:https://github.com/ir193/tiny_linux/blob/master/myconfig2
