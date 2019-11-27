### xshell知识点  

    xshell重新连接：ctrl+shift+r (插头连接标志)
    xshell断开： alt+c （断开插头）
    xshell所有快捷键： 工具栏---按键对应
    xshell 2个界面：工具栏---新建选项卡组
    全屏：alt+enter
    xshell中查找：  点击查找按钮
    撰写栏： 可以选择对所有的会话执行某个命令(慎用，可能会有正式的服务器，万一命令错了)
    xshell锁屏密码：和win7锁屏密码一样

##mysql查询名称是否重复  
不能使用querylist，因为list是模糊查询，而重复是完全匹配。

### dubbo重试次数：     注意是retries，不是retry  

    <dubbo:reference id="groupPortrayAnalysisService" registry="beijingRegistry"
		group="haier" owner="haier"
		interface="com.ehaier.crmbusiness.service.analysis.GroupPortrayAnalysisService"
		version="1.0.0" protocol="dubbo" timeout="${dubbo.reference.timeout}" init="true" retries="0"/>

### debug改变量：   
variables 视图，变量上右键---change value，输入表达式即可  如id=324L; (直接输入值是不行的)  

###
boot配置tomcat  

    1、三个pom都不能少：
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-tomcat</artifactId>
      <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.tomcat.embed</groupId>
        <artifactId>tomcat-embed-jasper</artifactId>
        <scope>provided</scope>
    </dependency>
    <dependency>
       <groupId>javax.servlet</groupId>
       <artifactId>javax.servlet-api</artifactId>
       <scope>provided</scope>
    </dependency>
    2、不要加入freemarker和thymeleaf
    3、application.properties中设置：
    spring.mvc.view.prefix=/WEB-INF/jsp/
    spring.mvc.view.suffix=.jsp


### springboot排除tomcat  

    <packaging>jar</packaging>   jar变成war
    <!--配置jsp jstl的支持-->
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>jstl</artifactId>
    </dependency>
    <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-tomcat</artifactId>
       <scope>provided</scope>
    </dependency>
    <dependency>
       <groupId>org.apache.tomcat.embed</groupId>
       <artifactId>tomcat-embed-jasper</artifactId>
       <scope>provided</scope>
    </dependency>
    然后配置：
    spring.mvc.view.prefix: /
    spring.mvc.view.suffix: .jsp

### DecimalFormat进行四舍五入  

    DecimalFormat decimalFormat = new DecimalFormat("0.00");
    uvPercentTotal=decimalFormat.format(new BigDecimal(uvTotal).divide(new BigDecimal(totalSum),2,BigDecimal.ROUND_HALF_DOWN).doubleValue());    //ROUND_HALF_DOWN是四舍五入  2是保留小数位

### dubbo服务缺失项目一定不能启动么   
不一定，如果项目中没有用到，但是dubbo-consumer.xml中配置了，只会报错，但是不影响项目启动，超时时间不能太长，否则等待不过来。

### inner join和left join的区别  
left join 一定要写on条件，否则报错。
inner join不写条件相当于a,b。
如果条件不匹配，可以返回0条。
left join最少会返回左表条数。

### mysql左外连接分析
最小条数，为l
最大条数,右表所有记录和左表中的一条记录匹配。
l+r-1
所以条数 为     l<=n<=l+r-1;

### poi(excel,hssf)  
    HSSFWorkbook wb = new HSSFWorkbook();   // 创建excel
    HSSFSheet sheet1 = wb.createSheet(SHEET1_NAME);  //创建sheet
    sheet1.createRow(i); // 创建行
    ------------------------------------
    fontA = wb.createFont(); //创建字体
    fontC.setColor(HSSFColor.BLACK.index); //创建
    fontC.setFontHeightInPoints((short)11); // 字体大小
    fontC.setBoldweight(HSSFFont.BOLDWEIGHT_BOLD);  //  粗体
    fontC.setFontName(FONT_NAME); // 字体名称
    -------------------------------------
    HSSFCellStyle cellStyle = wb.createCellStyle(); // 横向对齐方式
    cellStyle.setAlignment(hAlign); // 垂直居中
    cellStyle.setVerticalAlignment(HSSFCellStyle.VERTICAL_CENTER); // 填充色
    if(fillColorIdx != -1) {
    	cellStyle.setFillForegroundColor(fillColorIdx);
    	cellStyle.setFillPattern(HSSFCellStyle.SOLID_FOREGROUND);
    }
    cellStyle.setWrapText(true);
    cellStyle.setFont(font);
    --------------------------------------------

    RegionUtil.setLeftBorderColor(colorIdx, cellRangeAddress, sheet, wb); //regionUtil设置边框
    RegionUtil.setTopBorderColor(colorIdx, cellRangeAddress, sheet, wb); //
    RegionUtil.setRightBorderColor(colorIdx, cellRangeAddress, sheet, wb); //
    RegionUtil.setBottomBorderColor(colorIdx, cellRangeAddress, sheet, wb); //
    ---------------------------------------------
    复制样式：cloneStyleFrom
    --------------------------------------------
    复制单元格：
    private static void mergerRegion(HSSFSheet sheetCreat, HSSFSheet sheet) {
    		int sheetMergerCount = sheet.getNumMergedRegions();
    		System.out.println(sheetMergerCount);
    		for (int i = 0; i < sheetMergerCount; i++) {
    			CellRangeAddress mergedRegion = sheet.getMergedRegion(i);
    			if (mergedRegion.getNumberOfCells() >= 2) {
    				sheetCreat.addMergedRegion(mergedRegion);
    			}
    		}
    	}
    -----------------------------------------------
    复制内容并去掉空格：
    public static String removeInternalBlank(String s) {
    		Pattern p = Pattern.compile("\\s*|\t|\r|\n");
    		Matcher m = p.matcher(s);
    		char str[] = s.toCharArray();
    		StringBuffer sb = new StringBuffer();
    		for (int i = 0; i < str.length; i++) {
    			if (str[i] == ' ') {
    				sb.append(' ');
    			} else {
    				break;
    			}
    		}
    		String after = m.replaceAll("");
    		return sb.toString() + after;
    	}
    -----------------------------------------------
    复制行：
    int firstCell = row.getFirstCellNum();
    int lastCell = row.getLastCellNum();
    for (int j = firstCell; j < lastCell; j++) {
    }
