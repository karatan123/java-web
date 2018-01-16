######获取信息
```
package bean;

import java.net.InetAddress;  
import java.net.UnknownHostException;  
import java.text.DecimalFormat;  
  
import org.hyperic.sigar.CpuInfo;  
import org.hyperic.sigar.CpuPerc;  
import org.hyperic.sigar.FileSystem;  
import org.hyperic.sigar.FileSystemUsage;  
import org.hyperic.sigar.Mem;  
import org.hyperic.sigar.NetFlags;  
import org.hyperic.sigar.NetInterfaceConfig;  
import org.hyperic.sigar.NetInterfaceStat;  
import org.hyperic.sigar.OperatingSystem;  
import org.hyperic.sigar.Sigar;  
import org.hyperic.sigar.SigarException;  
import org.hyperic.sigar.SigarNotImplementedException;  
import org.hyperic.sigar.Swap;  
  
public class SysInfo {  
  
    public static void main(String [] args) throws Exception{  
        SysInfo s =new SysInfo();  
        System.out.println("CPU个数："+s.getCpuCount());  
        s.getCpuTotal();  
        s.testCpuPerc();  
        s.getPhysicalMemory();  
        s.testWho();  
        s.testFileSystemInfo();  
        s.testGetOSInfo();  
    }  
    /** 
     * 1.CPU资源信息 
     */  
      
    // a)CPU数量（单位：个）  
    public static int getCpuCount() throws SigarException {  
        Sigar sigar = new Sigar();  
        try {  
            return sigar.getCpuInfoList().length;  
        } finally {  
            sigar.close();  
        }  
    }  
  
    // b)CPU的总量（单位：HZ）及CPU的相关信息  
    public void getCpuTotal() {  
        Sigar sigar = new Sigar();  
        CpuInfo[] infos;  
        try {  
            infos = sigar.getCpuInfoList();  
            for (int i = 0; i < infos.length; i++) {// 不管是单块CPU还是多CPU都适用  
                CpuInfo info = infos[i];  
                System.out.println("CPU的总量:" + info.getMhz());// CPU的总量MHz  
                System.out.println("获得CPU的卖主：" + info.getVendor());// 获得CPU的卖主，如：Intel  
                System.out.println("CPU的类别：" + info.getModel());// 获得CPU的类别，如：Celeron  
                System.out.println("缓冲存储器数量：" + info.getCacheSize());// 缓冲存储器数量  
                System.out.println("**************");  
            }  
        } catch (SigarException e) {  
            e.printStackTrace();  
        }  
    }  
  
    // c)CPU的用户使用量、系统使用剩余量、总的剩余量、总的使用占用量等（单位：100%）  
    public void testCpuPerc() {  
        Sigar sigar = new Sigar();  
        // 方式一，主要是针对一块CPU的情况  
        CpuPerc cpu;  
        try {  
            cpu = sigar.getCpuPerc();  
            printCpuPerc(cpu);  
        } catch (SigarException e) {  
            e.printStackTrace();  
        }  
        // 方式二，不管是单块CPU还是多CPU都适用  
        CpuPerc cpuList[] = null;  
        try {  
            cpuList = sigar.getCpuPercList();  
        } catch (SigarException e) {  
            e.printStackTrace();  
            return;  
        }  
        for (int i = 0; i < cpuList.length; i++) {  
            printCpuPerc(cpuList[i]);  
        }  
    }  
  
    private void printCpuPerc(CpuPerc cpu) {  
        System.out.println("用户使用率:" + CpuPerc.format(cpu.getUser()));// 用户使用率  
        System.out.println("系统使用率:" + CpuPerc.format(cpu.getSys()));// 系统使用率  
        System.out.println("当前等待率:" + CpuPerc.format(cpu.getWait()));// 当前等待率  
        System.out.println("Nice :" + CpuPerc.format(cpu.getNice()));//  
        System.out.println("当前空闲率:" + CpuPerc.format(cpu.getIdle()));// 当前空闲率  
        System.out.println("总的使用率:" + CpuPerc.format(cpu.getCombined()));// 总的使用率  
        System.out.println("**************");  
    }  
  
    /** 
     * 2.内存资源信息 
     * 
     */  
      
    public void getPhysicalMemory() {  
        // a)物理内存信息  
        DecimalFormat df = new DecimalFormat("#0.00");  
        Sigar sigar = new Sigar();  
        Mem mem;  
        try {  
            mem = sigar.getMem();  
            // 内存总量  
            System.out.println("内存总量：" + df.format((float)mem.getTotal() / 1024/1024/1024) + "G");  
            // 当前内存使用量  
            System.out.println("当前内存使用量：" + df.format((float)mem.getUsed() / 1024/1024/1024) + "G");  
            // 当前内存剩余量  
            System.out.println("当前内存剩余量：" + df.format((float)mem.getFree() / 1024/1024/1024) + "G");  
            // b)系统页面文件交换区信息  
            Swap swap = sigar.getSwap();  
            // 交换区总量  
            System.out.println("交换区总量：" + df.format((float)swap.getTotal() / 1024/1024/1024) + "G");  
            // 当前交换区使用量  
            System.out.println("当前交换区使用量：" + df.format((float)swap.getUsed() / 1024/1024/1024) + "G");  
            // 当前交换区剩余量  
            System.out.println("当前交换区剩余量：" + df.format((float)swap.getFree() / 1024/1024/1024) + "G");  
        } catch (SigarException e) {  
            e.printStackTrace();  
        }  
    }  
  
    /** 
     * 3.操作系统信息 
     *  
     */  
      
    // a)取到当前操作系统的名称：  
    public String getPlatformName() {  
        String hostname = "";  
        try {  
            hostname = InetAddress.getLocalHost().getHostName();  
        } catch (Exception exc) {  
            Sigar sigar = new Sigar();  
            try {  
                hostname = sigar.getNetInfo().getHostName();  
            } catch (SigarException e) {  
                hostname = "localhost.unknown";  
            } finally {  
                sigar.close();  
            }  
        }  
        return hostname;  
    }  
  
    // b)取当前操作系统的信息  
    public void testGetOSInfo() {  
        OperatingSystem OS = OperatingSystem.getInstance();  
        // 操作系统内核类型如： 386、486、586等x86  
        System.out.println("OS.getArch() = " + OS.getArch());  
        System.out.println("OS.getCpuEndian() = " + OS.getCpuEndian());//  
        System.out.println("OS.getDataModel() = " + OS.getDataModel());//  
        // 系统描述  
        System.out.println("OS.getDescription() = " + OS.getDescription());  
        System.out.println("OS.getMachine() = " + OS.getMachine());//  
        // 操作系统类型  
        System.out.println("OS.getName() = " + OS.getName());  
        System.out.println("OS.getPatchLevel() = " + OS.getPatchLevel());//  
        // 操作系统的卖主  
        System.out.println("OS.getVendor() = " + OS.getVendor());  
        // 卖主名称  
        System.out  
                .println("OS.getVendorCodeName() = " + OS.getVendorCodeName());  
        // 操作系统名称  
        System.out.println("OS.getVendorName() = " + OS.getVendorName());  
        // 操作系统卖主类型  
        System.out.println("OS.getVendorVersion() = " + OS.getVendorVersion());  
        // 操作系统的版本号  
        System.out.println("OS.getVersion() = " + OS.getVersion());  
    }  
  
    // c)取当前系统进程表中的用户信息  
    public void testWho() {  
        try {  
            Sigar sigar = new Sigar();  
            org.hyperic.sigar.Who[] who = sigar.getWhoList();  
            if (who != null && who.length > 0) {  
                for (int i = 0; i < who.length; i++) {  
                    System.out.println("\n~~~~~~~~~" + String.valueOf(i)  
                            + "~~~~~~~~~");  
                    org.hyperic.sigar.Who _who = who[i];  
                    System.out.println("获取设备getDevice() = " + _who.getDevice());  
                    System.out.println("获得主机getHost() = " + _who.getHost());  
                    System.out.println("获取的时间getTime() = " + _who.getTime());  
                    // 当前系统进程表中的用户名  
                    System.out.println("获取用户getUser() = " + _who.getUser());  
                }  
            }  
        } catch (SigarException e) {  
            e.printStackTrace();  
        }  
    }  
  
    // 4.资源信息（主要是硬盘）  
    // a)取硬盘已有的分区及其详细信息（通过sigar.getFileSystemList()来获得FileSystem列表对象，然后对其进行编历）：  
    public void testFileSystemInfo() throws Exception {  
        Sigar sigar = new Sigar();  
        FileSystem fslist[] = sigar.getFileSystemList();  
        DecimalFormat df = new DecimalFormat("#0.00");  
        // String dir = System.getProperty("user.home");// 当前用户文件夹路径  
        for (int i = 0; i < fslist.length; i++) {  
            System.out.println("\n~~~~~~~~~~" + i + "~~~~~~~~~~");  
            FileSystem fs = fslist[i];  
            // 分区的盘符名称  
            System.out.println("fs.getDevName() = " + fs.getDevName());  
            // 分区的盘符名称  
            System.out.println("fs.getDirName() = " + fs.getDirName());  
            System.out.println("fs.getFlags() = " + fs.getFlags());//  
            // 文件系统类型，比如 FAT32、NTFS  
            System.out.println("fs.getSysTypeName() = " + fs.getSysTypeName());  
            // 文件系统类型名，比如本地硬盘、光驱、网络文件系统等  
            System.out.println("fs.getTypeName() = " + fs.getTypeName());  
            // 文件系统类型  
            System.out.println("fs.getType() = " + fs.getType());  
            FileSystemUsage usage = null;  
            try {  
                usage = sigar.getFileSystemUsage(fs.getDirName());  
            } catch (SigarException e) {  
                if (fs.getType() == 2)  
                    throw e;  
                continue;  
            }  
            switch (fs.getType()) {  
            case 0: // TYPE_UNKNOWN ：未知  
                break;  
            case 1: // TYPE_NONE  
                break;  
            case 2: // TYPE_LOCAL_DISK : 本地硬盘  
                // 文件系统总大小  
                System.out.println(" Total = " + df.format((float)usage.getTotal()/1024/1024) + "G");  
                // 文件系统剩余大小  
                System.out.println(" Free = " + df.format((float)usage.getFree()/1024/1024) + "G");  
                // 文件系统可用大小  
                System.out.println(" Avail = " + df.format((float)usage.getAvail()/1024/1024) + "G");  
                // 文件系统已经使用量  
                System.out.println(" Used = " + df.format((float)usage.getUsed()/1024/1024) + "G");  
                double usePercent = usage.getUsePercent() * 100D;  
                // 文件系统资源的利用率  
                System.out.println(" Usage = " + df.format(usePercent) + "%");  
                break;  
            case 3:// TYPE_NETWORK ：网络  
                break;  
            case 4:// TYPE_RAM_DISK ：闪存  
                break;  
            case 5:// TYPE_CDROM ：光驱  
                break;  
            case 6:// TYPE_SWAP ：页面交换  
                break;  
            }  
            System.out.println(" DiskReads = " + usage.getDiskReads());  
            System.out.println(" DiskWrites = " + usage.getDiskWrites());  
        }  
        return;  
    }  
  
    // 5.网络信息  
    // a)当前机器的正式域名  
    public String getFQDN() {  
        Sigar sigar = null;  
        try {  
            return InetAddress.getLocalHost().getCanonicalHostName();  
        } catch (UnknownHostException e) {  
            try {  
                sigar = new Sigar();  
                return sigar.getFQDN();  
            } catch (SigarException ex) {  
                return null;  
            } finally {  
                sigar.close();  
            }  
        }  
    }  
  
    // b)取到当前机器的IP地址  
    public String getDefaultIpAddress() {  
        String address = null;  
        try {  
            address = InetAddress.getLocalHost().getHostAddress();  
            // 没有出现异常而正常当取到的IP时，如果取到的不是网卡循回地址时就返回  
            // 否则再通过Sigar工具包中的方法来获取  
            if (!NetFlags.LOOPBACK_ADDRESS.equals(address)) {  
                return address;  
            }  
        } catch (UnknownHostException e) {  
            // hostname not in DNS or /etc/hosts  
        }  
        Sigar sigar = new Sigar();  
        try {  
            address = sigar.getNetInterfaceConfig().getAddress();  
        } catch (SigarException e) {  
            address = NetFlags.LOOPBACK_ADDRESS;  
        } finally {  
            sigar.close();  
        }  
        return address;  
    }  
  
    // c)取到当前机器的MAC地址  
    public String getMAC() {  
        Sigar sigar = null;  
        try {  
            sigar = new Sigar();  
            String[] ifaces = sigar.getNetInterfaceList();  
            String hwaddr = null;  
            for (int i = 0; i < ifaces.length; i++) {  
                NetInterfaceConfig cfg = sigar.getNetInterfaceConfig(ifaces[i]);  
                if (NetFlags.LOOPBACK_ADDRESS.equals(cfg.getAddress())  
                        || (cfg.getFlags() & NetFlags.IFF_LOOPBACK) != 0  
                        || NetFlags.NULL_HWADDR.equals(cfg.getHwaddr())) {  
                    continue;  
                }  
                /* 
                 * 如果存在多张网卡包括虚拟机的网卡，默认只取第一张网卡的MAC地址，如果要返回所有的网卡（包括物理的和虚拟的）则可以修改方法的返回类型为数组或Collection 
                 * ，通过在for循环里取到的多个MAC地址。 
                 */  
                hwaddr = cfg.getHwaddr();  
                break;  
            }  
            return hwaddr != null ? hwaddr : null;  
        } catch (Exception e) {  
            return null;  
        } finally {  
            if (sigar != null)  
                sigar.close();  
        }  
    }  
  
    // d)获取网络流量等信息  
    public void testNetIfList() throws Exception {  
        Sigar sigar = new Sigar();  
        String ifNames[] = sigar.getNetInterfaceList();  
        for (int i = 0; i < ifNames.length; i++) {  
            String name = ifNames[i];  
            NetInterfaceConfig ifconfig = sigar.getNetInterfaceConfig(name);  
            print("\nname = " + name);// 网络设备名  
            print("Address = " + ifconfig.getAddress());// IP地址  
            print("Netmask = " + ifconfig.getNetmask());// 子网掩码  
            if ((ifconfig.getFlags() & 1L) <= 0L) {  
                print("!IFF_UP...skipping getNetInterfaceStat");  
                continue;  
            }  
            try {  
                NetInterfaceStat ifstat = sigar.getNetInterfaceStat(name);  
                print("RxPackets = " + ifstat.getRxPackets());// 接收的总包裹数  
                print("TxPackets = " + ifstat.getTxPackets());// 发送的总包裹数  
                print("RxBytes = " + ifstat.getRxBytes());// 接收到的总字节数  
                print("TxBytes = " + ifstat.getTxBytes());// 发送的总字节数  
                print("RxErrors = " + ifstat.getRxErrors());// 接收到的错误包数  
                print("TxErrors = " + ifstat.getTxErrors());// 发送数据包时的错误数  
                print("RxDropped = " + ifstat.getRxDropped());// 接收时丢弃的包数  
                print("TxDropped = " + ifstat.getTxDropped());// 发送时丢弃的包数  
            } catch (SigarNotImplementedException e) {  
            } catch (SigarException e) {  
                print(e.getMessage());  
            }  
        }  
    }  
  
    void print(String msg) {  
        System.out.println(msg);  
    }  
  
    // e)一些其他的信息  
    public void getEthernetInfo() {  
        Sigar sigar = null;  
        try {  
            sigar = new Sigar();  
            String[] ifaces = sigar.getNetInterfaceList();  
            for (int i = 0; i < ifaces.length; i++) {  
                NetInterfaceConfig cfg = sigar.getNetInterfaceConfig(ifaces[i]);  
                if (NetFlags.LOOPBACK_ADDRESS.equals(cfg.getAddress())  
                        || (cfg.getFlags() & NetFlags.IFF_LOOPBACK) != 0  
                        || NetFlags.NULL_HWADDR.equals(cfg.getHwaddr())) {  
                    continue;  
                }  
                System.out.println("cfg.getAddress() = " + cfg.getAddress());// IP地址  
                System.out  
                        .println("cfg.getBroadcast() = " + cfg.getBroadcast());// 网关广播地址  
                System.out.println("cfg.getHwaddr() = " + cfg.getHwaddr());// 网卡MAC地址  
                System.out.println("cfg.getNetmask() = " + cfg.getNetmask());// 子网掩码  
                System.out.println("cfg.getDescription() = "  
                        + cfg.getDescription());// 网卡描述信息  
                System.out.println("cfg.getType() = " + cfg.getType());//  
                System.out.println("cfg.getDestination() = "  
                        + cfg.getDestination());  
                System.out.println("cfg.getFlags() = " + cfg.getFlags());//  
                System.out.println("cfg.getMetric() = " + cfg.getMetric());  
                System.out.println("cfg.getMtu() = " + cfg.getMtu());  
                System.out.println("cfg.getName() = " + cfg.getName());  
                System.out.println();  
            }  
        } catch (Exception e) {  
            System.out.println("Error while creating GUID" + e);  
        } finally {  
            if (sigar != null)  
                sigar.close();  
        }  
    }  
  
}  
```
######
1._time.java
```
package bean;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.jfree.chart.servlet.ServletUtilities;

public class _time extends HttpServlet {

	/**
	 * The doGet method of the servlet. <br>
	 *
	 * This method is called when a form has its tag value method equals to get.
	 * 
	 * @param request the request send by the client to the server
	 * @param response the response send by the server to the client
	 * @throws ServletException if an error occurred
	 * @throws IOException if an error occurred
	 */
	public void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {

		String fileName=ServletUtilities.saveChartAsJPEG(
				time.createChart(),600,300,request.getSession()
				);
	//	String graphURL=request.getContextPath()+"/DisplayChart?filename="+fileName;
	//	request.setAttribute("graphURL", graphURL);
	//	request.getRequestDispatcher("/time.jsp").forward(request, response);
		
		String graphURL=request.getContextPath()+"/servlet/DisplayChart?filename="+fileName;
		request.setAttribute("graphURL",graphURL);
		request.getRequestDispatcher("/time.jsp").forward(request,response);
	}

}
```
time.java
```
package bean;

import java.awt.Color;
import java.awt.Font;
import java.text.DateFormat;
import java.text.DecimalFormat;
import java.text.SimpleDateFormat;

import org.hyperic.sigar.Mem;
import org.hyperic.sigar.Sigar;
import org.hyperic.sigar.SigarException;
import org.hyperic.sigar.Swap;
import org.jfree.chart.ChartFactory;
import org.jfree.chart.JFreeChart;
import org.jfree.chart.axis.DateAxis;
import org.jfree.chart.axis.DateTickUnit;
import org.jfree.chart.axis.DateTickUnitType;
import org.jfree.chart.axis.ValueAxis;
import org.jfree.chart.plot.XYPlot;
import org.jfree.data.time.Day;
import org.jfree.data.time.TimeSeries;
import org.jfree.data.time.TimeSeriesCollection;
import org.jfree.data.xy.XYDataset;

public class time {
	private static final Font plot_=new Font("宋体",Font.ITALIC,18);
	
	public static XYDataset createDataset(){
		TimeSeries time=new TimeSeries("Data");
		Day day=new Day(1,1,2008);
		double d=3000D;
		for(int i=0;i<365;i++){
			d=d+(Math.random()-0.5)*10;
			time.add(day,d);
			day=(Day)day.next();
		}
		TimeSeriesCollection timeSeries=new TimeSeriesCollection(time);
		return timeSeries;
	}
	public static JFreeChart createChart(){
		JFreeChart chart=ChartFactory.createTimeSeriesChart(
				"销量统计",
				"月份",
				"销量",
				createDataset(),
				true,
				true,
				false
				);
		chart.getTitle().setFont(new Font("隶书",Font.BOLD,26));
		chart.setBackgroundPaint(new Color(252,175,134));
		XYPlot plot=chart.getXYPlot();
		plot.setDomainGridlinesVisible(false);
		DateAxis dataAxis=(DateAxis)plot.getDomainAxis();
		dataAxis.setLabelFont(new Font("黑体",Font.ITALIC,18));
		dataAxis.setTickLabelFont(new Font("宋体",Font.PLAIN,12));
		dataAxis.setLowerMargin(0.0);
		ValueAxis value=plot.getRangeAxis();
		value.setLabelFont(plot_);
		DateFormat format=new SimpleDateFormat("MM月份");
		DateTickUnit du=new DateTickUnit(DateTickUnitType.DAY,29,format);
		dataAxis.setTickUnit(du);
		return chart;
		
	}
}

```
######柱状图
-zhu
```
package bean;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.jfree.chart.servlet.ServletUtilities;

public class _zhu extends HttpServlet {

	/**
	 * The doGet method of the servlet. <br>
	 *
	 * This method is called when a form has its tag value method equals to get.
	 * 
	 * @param request the request send by the client to the server
	 * @param response the response send by the server to the client
	 * @throws ServletException if an error occurred
	 * @throws IOException if an error occurred
	 */
	public void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		String fileName=ServletUtilities.saveChartAsJPEG(
				zhu.createChart(),500,300,request.getSession()
				);
		String graphURL=request.getContextPath()+"/servlet/DisplayChart?filename="+fileName;
		request.setAttribute("graphURL",graphURL);
		request.getRequestDispatcher("/zhu.jsp").forward(request,response);
		
	}

}
```
zhu
```
package bean;

import java.awt.Font;
import java.awt.Image;
import java.io.IOException;
import java.text.DecimalFormat;

import javax.imageio.ImageIO;

import org.hyperic.sigar.FileSystem;
import org.hyperic.sigar.FileSystemUsage;
import org.hyperic.sigar.Mem;
import org.hyperic.sigar.Sigar;
import org.hyperic.sigar.SigarException;
import org.hyperic.sigar.Swap;
import org.jfree.chart.ChartFactory;
import org.jfree.chart.JFreeChart;
import org.jfree.chart.StandardChartTheme;
import org.jfree.chart.axis.CategoryAxis;
import org.jfree.chart.axis.CategoryLabelPositions;
import org.jfree.chart.axis.ValueAxis;
import org.jfree.chart.plot.CategoryPlot;
import org.jfree.chart.plot.PlotOrientation;
import org.jfree.chart.title.TextTitle;
import org.jfree.data.category.CategoryDataset;
import org.jfree.data.category.DefaultCategoryDataset;
import org.jfree.ui.VerticalAlignment;

import com.orsoncharts.renderer.category.BarRenderer3D;

public class zhu {
	public static CategoryDataset createDataSet(){
		DefaultCategoryDataset dataset=new DefaultCategoryDataset();
		DecimalFormat df=new DecimalFormat("#0.00");
		Sigar sigar=new Sigar();
		Mem mem;
		try{
			//内存
			mem=sigar.getMem();
	//		dataset.addValue(mem.getTotal() / 1024/1024/1024,"内存","总量");
		//	dataset.addValue(mem.getUsed()/1024/1024/1024,"内存","使用量");
		//	dataset.addValue(mem.getFree(),"内存","剩余量");
			//交换区
			Swap swap=sigar.getSwap();
			dataset.addValue(swap.getTotal()/1024/1024/1024,"交换区","总量");
			dataset.addValue(swap.getUsed()/1024/1024/1024,"交换区","使用量");
			dataset.addValue(swap.getFree()/1024/1024/1024,"交换区","剩余量");
	/*		//硬盘 
		    FileSystem fslist[] = sigar.getFileSystemList();  
		    for(int i=0;i<fslist.length;i++){
		    	FileSystem fs=fslist[i];
		    	FileSystemUsage usage=null;
		    	usage=sigar.getFileSystemUsage(fs.getDirName());
		    	 switch (fs.getType()) {  
		            case 0: // TYPE_UNKNOWN ：未知  
		                break;  
		            case 1: // TYPE_NONE  
		                break;  
		            case 2: // TYPE_LOCAL_DISK : 本地硬盘  
		                // 文件系统总大小  
		               dataset.addValue(usage.getTotal()/1024/1024,"文件系统大小","总量");
		                // 文件系统可用大小  
		                dataset.addValue(usage.getAvail()/1024/1024,"文件系统大小","使用量");
		                // 文件系统已经使用量  
		             dataset.addValue( usage.getUsed()/1024/1024,"文件系统大小","剩余量");   
		                break;  
		            case 3:// TYPE_NETWORK ：网络  
		                break;  
		            case 4:// TYPE_RAM_DISK ：闪存  
		                break;  
		            case 5:// TYPE_CDROM ：光驱  
		                break;  
		            case 6:// TYPE_SWAP ：页面交换  
		                break;  
		            }  
		    }*/
		}catch(SigarException e){
			e.printStackTrace();
		}
		
		return dataset;
	}
	public static JFreeChart createChart(){
		
		StandardChartTheme stand=new StandardChartTheme("CN");
		stand.setExtraLargeFont(new Font("隶书",Font.BOLD,20));
		stand.setRegularFont(new Font("宋体",Font.PLAIN,15));
		stand.setLargeFont(new Font("宋体",Font.PLAIN,15));
		ChartFactory.setChartTheme(stand);    
		JFreeChart ch=ChartFactory.createBarChart3D(
				"电脑内存和交换区信息",
				"内存/交换区",
				"量",
				createDataSet(),
				PlotOrientation.VERTICAL,
				true,
				false,
				false
				);
	/*	Image image=null;
		try{
			image=ImageIO.read(ChartUtil.class.getResource("test.JPG"));
		}catch(IOException e){
			e.printStackTrace();
		}
		ch.getTitle().setFont(new Font("隶书",Font.BOLD,25));
		ch.getLegend().setItemFont(new Font("宋体",Font.PLAIN,12));
		ch.setBorderVisible(true);
		TextTitle subTitle=new TextTitle("本机信息（内存,交换区，文件）");
		subTitle.setVerticalAlignment(VerticalAlignment.BOTTOM);
		ch.addSubtitle(subTitle);
		CategoryPlot plot=ch.getCategoryPlot();
		plot.setForegroundAlpha(.08F);
		plot.setBackgroundAlpha(0.5F);
		plot.setBackgroundImage(image);
		CategoryAxis categoryAxis=plot.getDomainAxis();
		categoryAxis.setLabelFont(new Font("宋体",Font.PLAIN,12));
		categoryAxis.setTickLabelFont(new Font("宋体",Font.PLAIN,12));
		categoryAxis.setCategoryLabelPositions(CategoryLabelPositions.UP_45);
		ValueAxis valueAxis=plot.getRangeAxis();
		valueAxis.setLabelFont(new Font("宋体",Font.PLAIN,12));
		BarRenderer3D renderer=new BarRenderer3D();
	//	renderer.setItemMargin(0.32);
	//	plot.setRenderer(renderer);*/
		return ch;
		}
	
}

```
zhu.jsp
```
<%@ page language="java" import="java.util.*" pageEncoding="utf-8"%>
<%
String path = request.getContextPath();
String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";
%>
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
  <head>
    <base href="<%=basePath%>">
    
    <title>My JSP 'zhu.jsp' starting page</title>
    
	<meta http-equiv="pragma" content="no-cache">
	<meta http-equiv="cache-control" content="no-cache">
	<meta http-equiv="expires" content="0">    
	<meta http-equiv="keywords" content="keyword1,keyword2,keyword3">
	<meta http-equiv="description" content="This is my page">
	<!--
	<link rel="stylesheet" type="text/css" href="styles.css">
	-->

  </head>
  
  <body>
    	<div align="center">
    		<img src="${graphURL }" border="1">
    		<br><br>
    		<a href="quyu.jsp">返回</a>
    	</div>
  </body>
</html>

```
quyu.jsp
```
<%@ page language="java" import="java.util.*" pageEncoding="utf-8"%>
<%
String path = request.getContextPath();
String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";
%>

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
  <head>
    <base href="<%=basePath%>">
    
    <title>My JSP 'quyu.jsp' starting page</title>
    
	<meta http-equiv="pragma" content="no-cache">
	<meta http-equiv="cache-control" content="no-cache">
	<meta http-equiv="expires" content="0">    
	<meta http-equiv="keywords" content="keyword1,keyword2,keyword3">
	<meta http-equiv="description" content="This is my page">
	<!--
	<link rel="stylesheet" type="text/css" href="styles.css">
	-->

  </head>
  
  <body>
    <div align="center">
    	<a href="servlet/quyu">区域图</a><br>
    	<a href="servlet/_time">时序图</a><br>
    	<a href="servlet/_zhu">柱状图</a>
    </div>
  </body>
</html>

```
######区域图
quyu_jfree.java
```
package bean;

import java.awt.Color;
import java.awt.Font;
import java.text.DecimalFormat;
import java.util.Random;

import org.hyperic.sigar.Mem;
import org.hyperic.sigar.Sigar;
import org.hyperic.sigar.SigarException;
import org.hyperic.sigar.Swap;
import org.jfree.chart.ChartFactory;
import org.jfree.chart.JFreeChart;
import org.jfree.chart.plot.CategoryPlot;
import org.jfree.chart.plot.PlotOrientation;
import org.jfree.data.category.CategoryDataset;
import org.jfree.data.category.DefaultCategoryDataset;

public class quyu_jfree {
	private static final Font plot_font=new Font("宋体",Font.BOLD,15);
	public static CategoryDataset createDataset(){
	DefaultCategoryDataset defau=new DefaultCategoryDataset();
	Random random=new Random();
	for(int i=1;i<7;i++){
		defau.addValue(random.nextInt(5000),"移动一",i+"月份");
		defau.addValue(random.nextInt(5000),"移动二",i+"月份");
		defau.addValue(random.nextInt(5000),"移动三",i+"月份");
	}
	//
	
	
	return defau;
	}
	public static JFreeChart createChart(){
		JFreeChart chart=ChartFactory.createAreaChart(
				"网站流量统计分析",
				"网站",
				"流量",
				createDataset(),
				PlotOrientation.VERTICAL,
				true,
				true,
				false
				);
		chart.getTitle().setFont(new Font("隶书",Font.BOLD,25));
		chart.getLegend().setItemFont(new Font("宋体",Font.BOLD,15));
		chart.setBackgroundPaint(new Color(160,214,248));
		CategoryPlot plot=chart.getCategoryPlot();
		plot.getDomainAxis().setLabelFont(plot_font);
		plot.getDomainAxis().setTickLabelFont(plot_font);
		plot.getDomainAxis().setLabelFont(plot_font);
		plot.setForegroundAlpha(0.4F);
		plot.setDomainGridlinesVisible(true);
		return chart;
		
	}
}

```
quyu.java
```
package bean;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.jfree.chart.servlet.ServletUtilities;

public class quyu extends HttpServlet {

	/**
	 * The doGet method of the servlet. <br>
	 *
	 * This method is called when a form has its tag value method equals to get.
	 * 
	 * @param request the request send by the client to  server
	 * @param response the response send by the server to the client
	 * @throws ServletException if an error occurred
	 * @throws IOException if an error occurred
	 */
	public void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		String fileName=ServletUtilities.saveChartAsJPEG(
				quyu_jfree.createChart(),500,300,request.getSession()
				);
		String graphURL=request.getContextPath()+"/servlet/DisplayChart?filename="+fileName;
		request.setAttribute("graphURL",graphURL);
		request.getRequestDispatcher("/_quyu.jsp").forward(request,response);
	}

}

```
######数据库
jfree_jdbc.java
```
package bean;

import java.awt.Font;
import java.sql.SQLException;
import java.text.NumberFormat;

import org.jfree.chart.ChartFactory;
import org.jfree.chart.JFreeChart;
import org.jfree.chart.labels.StandardPieSectionLabelGenerator;
import org.jfree.chart.plot.PiePlot;
import org.jfree.data.general.PieDataset;
import org.jfree.data.jdbc.JDBCPieDataset;

public class jfree_jdbc {
	public static PieDataset initPieData() {  
        //数据库驱动  
        String driverName = "com.mysql.jdbc.Driver";  
        //数据库连接URL  
        String url = "jdbc:mysql://localhost:3306/tb_shop";  
        String user = "root";       //数据库用户名  
        String password = "zhj1124.";    //数据库密码  
        JDBCPieDataset dataset = null;  //数据集合  
        try {  
            //通过JDBC创建数据集合  
            dataset = new JDBCPieDataset(url,
driverName, user, password);  
            // SQL语句  
            String query = "select category,val from aaa";  
            //查询并向数据集合中添加数据  
            dataset.executeQuery(query);  
            //关闭数据库连接  
            dataset.close();  
        } catch (Exception e) {  
            e.printStackTrace();  
        }   
        return dataset;  
    }  
    /**  
     * 创建饼形图实例  
     * @return JFreeChart对象  
     */ 
    public static JFreeChart createChart() {  
        //创建3D饼形图表  
        JFreeChart chart = ChartFactory.createPieChart3D(  
                "XX商城月销量统计",  
//图表标题  
                initPieData(),  
        //饼形图的数据集对象  
                true,  
                //是否显示图例  
                true,  
                //是否显示提示文本  
                false);  
            //是否生成超链接  
        //设置标题字体  
        chart.getTitle().setFont(new Font("隶书",Font.BOLD,25));  
        //设置图例类别字体  
        chart.getLegend().setItemFont(new Font("宋体",Font.BOLD,15));  
        //获取绘图区对象  
        PiePlot plot = (PiePlot) chart.getPlot();   
        plot.setForegroundAlpha(0.5f);  
//设置前景透明度  
        //设置分类标签的字体  
        plot.setLabelFont(new Font("宋体",Font.PLAIN,12));  
        plot.setCircular(true);  
//设置饼形为正圆  
        //设置分类标签的格式  
        plot.setLabelGenerator(new 
StandardPieSectionLabelGenerator("{0}={2}",  
                NumberFormat.getNumberInstance(),  
                NumberFormat.getPercentInstance()));  
        return chart;  
    }  
} 
```
######选择区域图
imageServlet.java
```
package bean;

import java.awt.BasicStroke;
import java.awt.Color;
import java.awt.Font;
import java.io.IOException;
import java.util.Random;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.jfree.chart.ChartFactory;
import org.jfree.chart.JFreeChart;
import org.jfree.chart.plot.CategoryPlot;
import org.jfree.chart.plot.PlotOrientation;
import org.jfree.chart.renderer.category.LineAndShapeRenderer;
import org.jfree.chart.servlet.ServletUtilities;
import org.jfree.data.category.CategoryDataset;
import org.jfree.data.category.DefaultCategoryDataset;

/**
 * 使用JFreeChart绘制2D和3D折线图
 * @create Jun 25, 2013 9:58:11 PM
 * @author 玄玉<http://blog.csdn.net/jadyer>
 */
public class ImageServlet extends HttpServlet {
	private static final long serialVersionUID = -2942367547538171657L;

	public void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		//显示样式(是否为3D效果)
		String style = request.getParameter("style");
		//生成的折线图的文件名
		String imageName = null;
		if(null!=style && "3D".equals(style)){
			//ChartUtilities.writeChartAsJPEG()是面向Java Application的
			//ServletUtilities.saveChartAsPNG()是面向Web开发的
			imageName = ServletUtilities.saveChartAsJPEG(createChart(true), 500, 300, request.getSession());
		}else{
			//saveChartAsPNG()的返回值是生成的图片的名字,它所生成的图片会保存在服务器的临时目录下
			//Tomcat6的临时目录是D:/Develop/apache-tomcat-6.0.36/temp/目录 
			imageName = ServletUtilities.saveChartAsJPEG(createChart(false), 500, 300, request.getSession());
		}
		//获取图片的路径(此时JFreechart会根据filename到服务器的临时目录中寻找图片)
		String imageURL = request.getContextPath() + "/servlet/DisplayChart?filename=" + imageName;
		request.setAttribute("imageURL", imageURL);
		request.getRequestDispatcher("/result.jsp").forward(request, response);
	}
	
	
	/**
	 * 创建数据集
	 */
	private CategoryDataset createDataSet() {
		//图例名称
		String[] line = {"kaspersky", "Nod32", "360"};
		//类别
		String[] category = {"2008年", "2009年", "2010年", "2011年", "2012年"};
		DefaultCategoryDataset dataSet = new DefaultCategoryDataset();
		//向数据集中添加数据
		for(int i=0; i<line.length; i++){
			for(int j=0; j<category.length; j++){
				dataSet.addValue(100000 + new Random().nextInt(100000), line[i], category[j]);
			}
		}
		return dataSet;
	}
	/**
	 * 生成制图对象
	 * @param is3D 是否为3D效果
	 */
	private JFreeChart createChart(boolean is3D){
		JFreeChart chart = null;
		if(is3D){
			//图表标题,X轴标题,Y轴标题,绘图数据集,绘制方向,显示图例,采用标准生成器,生成链接
			chart = ChartFactory.createLineChart3D("2008-2012年优秀杀毒软件杀毒数量统计", "杀毒软件", "查杀病毒数量",
												   this.createDataSet(), PlotOrientation.VERTICAL, true, true, false);
		}else{
			chart = ChartFactory.createLineChart("2008-2012年优秀杀毒软件杀毒数量统计", "杀毒软件", "查杀病毒数量",
												 this.createDataSet(), PlotOrientation.VERTICAL, true, true, false);
		}
		chart.getTitle().setFont(new Font("隶书", Font.BOLD, 23));      //设置标题字体
		chart.getLegend().setItemFont(new Font("宋体", Font.BOLD, 15)); //设置图例类别字体
		chart.setBackgroundPaint(new Color(192, 228, 106));            //设置背景色
		CategoryPlot plot = chart.getCategoryPlot();                           //获取绘图区对象
		plot.getDomainAxis().setLabelFont(new Font("宋体", Font.BOLD, 15));     //设置横轴字体
		plot.getDomainAxis().setTickLabelFont(new Font("宋体", Font.BOLD, 15)); //设置坐标轴标尺值字体
		plot.getRangeAxis().setLabelFont(new Font("宋体", Font.BOLD, 15));      //设置纵轴字体
		plot.setBackgroundPaint(Color.WHITE);   //设置绘图区背景色
		plot.setRangeGridlinePaint(Color.RED);  //设置水平方向背景线颜色
		plot.setRangeGridlinesVisible(true);    //设置是否显示水平方向背景线,默认值为true
		plot.setDomainGridlinePaint(Color.RED); //设置垂直方向背景线颜色
		plot.setDomainGridlinesVisible(true);   //设置是否显示垂直方向背景线,默认值为false
		LineAndShapeRenderer renderer = (LineAndShapeRenderer)plot.getRenderer(); //获取折线对象
		BasicStroke realLine = new BasicStroke(1.6f); //设置实线
		float dashes[] = {8.0f};                      //定义虚线数组
		//线条粗细,端点风格,折点风格,折点处理办法,虚线数组,虚线偏移量
		BasicStroke brokenLine = new BasicStroke(1.6f, BasicStroke.CAP_SQUARE, BasicStroke.JOIN_MITER, 8.0f, dashes, 0.0f);
		renderer.setSeriesStroke(1, brokenLine); //利用虚线绘制
		renderer.setSeriesStroke(2, brokenLine); //利用虚线绘制
		renderer.setSeriesStroke(3, realLine);   //利用实线绘制
		return chart;
	}
}
```
result.jsp
```
<%@ page language="java" pageEncoding="UTF-8"%>
<img src="${imageURL}" border="1"/>
<br/><br/>
<h2><a href="<%=request.getContextPath()%>/index.jsp">返回</a></h2>

```
