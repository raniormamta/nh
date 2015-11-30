import java.io.IOException;

import org.xml.sax.SAXException;
import org.xml.sax.XMLReader;
import org.xml.sax.helpers.XMLReaderFactory;


public class Driver {
	
		public static void main(String[] args) throws IOException,SAXException {
		XMLReader p = XMLReaderFactory.createXMLReader();
		p.setContentHandler(new ShHd());
		p.parse("D:\\SidhiVinayak\\3-12-2015\\Sample\\src\\ACS.xml");
		ShHd sh=new ShHd();
		}

}


import java.io.IOException;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

import javax.xml.parsers.ParserConfigurationException;
import javax.xml.parsers.SAXParser;
import javax.xml.parsers.SAXParserFactory;

import org.xml.sax.Attributes;
import org.xml.sax.SAXException;
import org.xml.sax.helpers.DefaultHandler;


public class ShiftHandler extends DefaultHandler{

	List myFooters;
	List myHeaders;
	List myApps;
	
	private String tempVal;
	private String tempValu;
	private String tempValue;
	
	//to maintain context
	private Footer tempFooter;
	private Header tempHeader;
	private App tempApp;
	
	public ShiftHandler(){
		myFooters = new ArrayList();
		myHeaders = new ArrayList();
		myApps = new ArrayList();
	}
	
	public void runExample() {
		parseDocument();
		printData();
	}

	private void parseDocument() {
		
		//get a factory
		SAXParserFactory spf = SAXParserFactory.newInstance();
		try {
		
			//get a new instance of parser
			SAXParser sp = spf.newSAXParser();
			
			//parse the file and also register this class for call backs
			sp.parse("D:\\SidhiVinayak\\3-12-2015\\Sample\\src\\ACS.xml", this);
			
		}catch(SAXException se) {
			se.printStackTrace();
		}catch(ParserConfigurationException pce) {
			pce.printStackTrace();
		}catch (IOException ie) {
			ie.printStackTrace();
		}
	}

	/**
	 * Iterate through the list and print
	 * the contents
	 */
	private void printData(){
		
		System.out.println("No of RecordCount '" + myFooters.size() + "'.");
		Iterator it = myFooters.iterator();
		while(it.hasNext()) {
			System.out.println(it.next().toString());
		}
		
		System.out.println("No of Headers '" + myHeaders.size() + "'.");
		Iterator itr = myHeaders.iterator();
		while(itr.hasNext()) {
			System.out.println(itr.next().toString());
		}
		
		/*System.out.println("No of Headers '" + myHeaders.size() + "'.");
		Iterator it1 = myHeaders.iterator();
		while(it1.hasNext()) {
			System.out.println(it1.next().toString());
		}*/
		
	}
	

	//Event Handlers
	public void startElement(String uri, String localName, String qName, Attributes attributes) throws SAXException {
		//reset
		tempVal = "";
		if(qName.equalsIgnoreCase("Footer")) {
			//create a new instance of employee
			tempFooter = new Footer();
	//		tempFtr.setType(attributes.getValue("type"));
		}
	}
	

	public void characters(char[] ch, int start, int length) throws SAXException {
		tempVal = new String(ch,start,length);
	}
	
	public void endElement(String uri, String localName, String qName) throws SAXException {

		if(qName.equalsIgnoreCase("Footer")) {
			//add it to the list
			myFooters.add(tempFooter);
		}else if (qName.equalsIgnoreCase("RecordCount")) {
			tempFooter.setRecordCount(Integer.parseInt(tempVal));
		}
		
	}

	
	public void saveRecord() {
		try {
		Class.forName("oracle.jdbc.driver.OracleDriver");  
     	System.out.println("Loding Driver Class");
    //step2 create  the connection object  
    Connection con=DriverManager.getConnection(  
    "jdbc:oracle:thin:@192.168.2.68:1521:orcl","test","test");  
    	System.out.println("Connection created");
    //step3 create the statement object  
    	
    Statement stmt=con.createStatement();  
    	System.out.println("Creating Statment");
    //step4 execute query  
    ResultSet rs=stmt.executeQuery("desc fr"); 
    	System.out.println("Table Created");
    //while(rs.next())  
    	// System.out.println("hello_data");
    //System.out.println(rs.getInt(1)+"  "+rs.getString(2)+"  "+rs.getString(3));  
      
    //step5 close the connection object  
    
    
    
    }catch(Exception e){ System.out.println(e);
    e.printStackTrace();}  
      
    } 
	
	public static void main(String[] args){
		ShiftHandler sh = new ShiftHandler();
		sh.runExample();
	}
	
}


import java.util.Date;


public class Header {
	private long hPId;
	private String approvedFor;
	private String brandAAIAID;
	private String company;
	private String docFormNumber;
	private String documentTitle;
	private Date effectiveDate;
	private String mapperCompany;
	private String mapperContact;
	private String mapperEmail;
	private long mapperPhone;
	private int mapperPhoneExt;
	private Date pcdbVersionDate;
	private Date qdbVersionDate;
	private String senderName;
	private long senderPhone;
	private int senderPhoneExt;
	private String submissionType;
	private Date transferDate;
	private Date vcdbVersionDate;
	public Header() {
		super();
		// TODO Auto-generated constructor stub
	}
	public Header(long hPId, String approvedFor, String brandAAIAID,
			String company, String docFormNumber, String documentTitle,
			Date effectiveDate, String mapperCompany, String mapperContact,
			String mapperEmail, long mapperPhone, int mapperPhoneExt,
			Date pcdbVersionDate, Date qdbVersionDate, String senderName,
			long senderPhone, int senderPhoneExt, String submissionType,
			Date transferDate, Date vcdbVersionDate) {
		super();
		this.hPId = hPId;
		this.approvedFor = approvedFor;
		this.brandAAIAID = brandAAIAID;
		this.company = company;
		this.docFormNumber = docFormNumber;
		this.documentTitle = documentTitle;
		this.effectiveDate = effectiveDate;
		this.mapperCompany = mapperCompany;
		this.mapperContact = mapperContact;
		this.mapperEmail = mapperEmail;
		this.mapperPhone = mapperPhone;
		this.mapperPhoneExt = mapperPhoneExt;
		this.pcdbVersionDate = pcdbVersionDate;
		this.qdbVersionDate = qdbVersionDate;
		this.senderName = senderName;
		this.senderPhone = senderPhone;
		this.senderPhoneExt = senderPhoneExt;
		this.submissionType = submissionType;
		this.transferDate = transferDate;
		this.vcdbVersionDate = vcdbVersionDate;
	}
	public long gethPId() {
		return hPId;
	}
	public void sethPId(long hPId) {
		this.hPId = hPId;
	}
	public String getApprovedFor() {
		return approvedFor;
	}
	public void setApprovedFor(String approvedFor) {
		this.approvedFor = approvedFor;
	}
	public String getBrandAAIAID() {
		return brandAAIAID;
	}
	public void setBrandAAIAID(String brandAAIAID) {
		this.brandAAIAID = brandAAIAID;
	}
	public String getCompany() {
		return company;
	}
	public void setCompany(String company) {
		this.company = company;
	}
	public String getDocFormNumber() {
		return docFormNumber;
	}
	public void setDocFormNumber(String docFormNumber) {
		this.docFormNumber = docFormNumber;
	}
	public String getDocumentTitle() {
		return documentTitle;
	}
	public void setDocumentTitle(String documentTitle) {
		this.documentTitle = documentTitle;
	}
	public Date getEffectiveDate() {
		return effectiveDate;
	}
	public void setEffectiveDate(Date effectiveDate) {
		this.effectiveDate = effectiveDate;
	}
	public String getMapperCompany() {
		return mapperCompany;
	}
	public void setMapperCompany(String mapperCompany) {
		this.mapperCompany = mapperCompany;
	}
	public String getMapperContact() {
		return mapperContact;
	}
	public void setMapperContact(String mapperContact) {
		this.mapperContact = mapperContact;
	}
	public String getMapperEmail() {
		return mapperEmail;
	}
	public void setMapperEmail(String mapperEmail) {
		this.mapperEmail = mapperEmail;
	}
	public long getMapperPhone() {
		return mapperPhone;
	}
	public void setMapperPhone(long mapperPhone) {
		this.mapperPhone = mapperPhone;
	}
	public int getMapperPhoneExt() {
		return mapperPhoneExt;
	}
	public void setMapperPhoneExt(int mapperPhoneExt) {
		this.mapperPhoneExt = mapperPhoneExt;
	}
	public Date getPcdbVersionDate() {
		return pcdbVersionDate;
	}
	public void setPcdbVersionDate(Date pcdbVersionDate) {
		this.pcdbVersionDate = pcdbVersionDate;
	}
	public Date getQdbVersionDate() {
		return qdbVersionDate;
	}
	public void setQdbVersionDate(Date qdbVersionDate) {
		this.qdbVersionDate = qdbVersionDate;
	}
	public String getSenderName() {
		return senderName;
	}
	public void setSenderName(String senderName) {
		this.senderName = senderName;
	}
	public long getSenderPhone() {
		return senderPhone;
	}
	public void setSenderPhone(long senderPhone) {
		this.senderPhone = senderPhone;
	}
	public int getSenderPhoneExt() {
		return senderPhoneExt;
	}
	public void setSenderPhoneExt(int senderPhoneExt) {
		this.senderPhoneExt = senderPhoneExt;
	}
	public String getSubmissionType() {
		return submissionType;
	}
	public void setSubmissionType(String submissionType) {
		this.submissionType = submissionType;
	}
	public Date getTransferDate() {
		return transferDate;
	}
	public void setTransferDate(Date transferDate) {
		this.transferDate = transferDate;
	}
	public Date getVcdbVersionDate() {
		return vcdbVersionDate;
	}
	public void setVcdbVersionDate(Date vcdbVersionDate) {
		this.vcdbVersionDate = vcdbVersionDate;
	}
	@Override
	public String toString() {
		return "Header [approvedFor=" + approvedFor + ", brandAAIAID="
				+ brandAAIAID + ", company=" + company + ", docFormNumber="
				+ docFormNumber + ", documentTitle=" + documentTitle
				+ ", hPId=" + hPId + ", mapperCompany=" + mapperCompany
				+ ", mapperContact=" + mapperContact + ", mapperEmail="
				+ mapperEmail + ", mapperPhone=" + mapperPhone
				+ ", mapperPhoneExt=" + mapperPhoneExt + ", senderName="
				+ senderName + ", senderPhone=" + senderPhone
				+ ", senderPhoneExt=" + senderPhoneExt + ", submissionType="
				+ submissionType + "]";
	}
	
}



public class Footer {
	private long fPId;
	private long recordCount;
	public Footer() {
		super();
		// TODO Auto-generated constructor stub
	}
	public Footer(long fPId, long recordCount) {
		super();
		this.fPId = fPId;
		this.recordCount = recordCount;
	}
	public long getfPId() {
		return fPId;
	}
	public void setfPId(long fPId) {
		this.fPId = fPId;
	}
	public long getRecordCount() {
		return recordCount;
	}
	public void setRecordCount(long recordCount) {
		this.recordCount = recordCount;
	}
	@Override
	public String toString() {
		return "Footer [fPId=" + fPId + ", recordCount=" + recordCount + "]";
	}
}



public class App {
	public class ACES {
		private long acPId;
		private float version;
		}
	public class App {
		private long aPId;
		private String appAction;
		private long appId;
		private long appRef;
		private long appValidate;
		private long assetItemOrder;
		private String assetItemRef;
		private String assetItemName;
		private long displayOrder;
		private String mfrLabel;
		private String note;
		private long noteId;
		private String noteLang;
		private String partBrandAAIAId;
		private long partTypeId;
		private long positionId;
		private long qualId;
		private String qParamUom;
		private long qParamValue;
		private String qPText;
		private long qty;
		}
	
	public class Asset {
		private long AssetPId;
		private String assetAction;
		private String assetId;
		private String assetRef;
		private String assetValidate;
		}
	
	
	
	
	
	
	public class Header {
		
		}
]


package p1;
public class SAXSave {
public static void main(String args[]) {
System.out.println(p1.ShiftHandler.class.getMethods());
}
}
package p1;
import org.xml.sax.helpers.DefaultHandler;
import org.xml.sax.Attributes;
import org.xml.sax.SAXException;



public class VehAttr {
	private long VPId;
	private long aspirationId;
	private long baseVehicleId;
	private long bedLengthId;
	private long bedTypeId;
	private long bodyNumDoorsId;
	private long bodyTypeId;
	private long brakeABSId;
	private long brakeSystemId;
	private long cylinderHeadTypeId;
	private long driveTypeId;
	private long engineBaseId;
	private long engineDesignationId;
	private long engineMfrId;
	private long engineVersionId;
	private long engineVINId;
	private long frontBrakeTypeId;
	private long frontSpringTypeId;
	private long fuelDeliverySubTypeId;
	private long fuelDeliveryTypeId;
	private long fuelSystemControlTypeId;
	private long fuelSystemDesignId;
	private long fuelTypeId;
	@SuppressWarnings("unused")
	private long ignitionSystemTypeId;
	private long makeId;
	private long mfrBodyCodeId;
	private long modelId;
	private long powerOutputId;
	private long rearBrakeTypeId;
	private long rearSpringTypeId;
	private long regionId;
	private long steeringTypeId;
	private long steeringSystemId;
	private long subModelId;
	private long transElecContolledId;
	private long transmissionMfrId;
	private long transmissionMfrCodeId;
	private long transmissionBaseId;
	private long transmissionControlTypeId;
	private long transmissionNumSpeedsId;
	private long transmissionTypeId;
	private long valvesPerEngineId;
	private long vehicleTypeId;
	private long wheelBaseId;
	private long yearsFrom;
	private long yearsTo;
	}

}


import org.xml.sax.Attributes;
import org.xml.sax.SAXException;
import org.xml.sax.helpers.DefaultHandler;


public class ShHd extends DefaultHandler {
	public void startDocument() {
		System.out.println("Begin Parsing Document....");
		}
		public void endDocument() {
		System.out.println("\n End Parsing Document...");
		}
		public void startElement(String nameSpaceURI,String localName, String qName, Attributes atts){
		String elementName = qName;
		//System.out.println(nameSpaceURI);
		//System.out.println(localName);
		//System.out.println(qName);
		//System.out.println(atts);
		if (!"".equals(nameSpaceURI) && !"".equals(localName))
		elementName = nameSpaceURI + ":" + localName;
		System.out.print(elementName+" ");
		if (atts != null && atts.getLength() > 0) {
		for (int i = 0; i < atts.getLength(); i++)
		System.out.print(" "+atts.getLocalName(i)+" = "+atts.getValue(i)+" ");
		}
		}
		public void endElement(String nameSpaceURI, String localName, String qName) {
		System.out.print(qName);
		}
		public void characters(char []ch, int start, int length) throws SAXException
		{
		for(int i=start;i<(start+length);i++) {
		System.out.print(ch[i]);
		}
		}
		@Override
		public String toString() {
		return "ShHd []";
		}
		}




