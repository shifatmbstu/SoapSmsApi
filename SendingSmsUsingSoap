import java.io.ByteArrayInputStream;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.io.StringWriter;
import java.nio.charset.Charset;

import javax.xml.soap.*;
import javax.xml.transform.*;
import javax.xml.transform.stream.*;

import org.w3c.dom.NodeList;

public class SendSms {

    /**
     * Starting point for the SAAJ - SOAP Client Testing
     * @author Shifatul  Islam
     * shifat.it@gmail.com
     * +8801745944843
     * MIT SMS SOAP Service  BANGLADESH MICROTECHNOLOGY LTD
     */
    public static void main(String args[]) {
        try {
            SOAPConnectionFactory soapConnectionFactory = SOAPConnectionFactory.newInstance();
            SOAPConnection soapConnection = soapConnectionFactory.createConnection();
            String url = "http://27.147.137.181/M2BWS_SMS.asmx";
            
            //login
            SOAPMessage soapResponse = soapConnection.call(buildLogin(), url);
            printSOAPResponse(soapResponse);
            //send text message
            SOAPMessage soapResponseTextFs = soapConnection.call(buildSoapMessageTextFs(), url);
            printSOAPResponse(soapResponseTextFs);
            
            soapConnection.close();
        } catch (Exception e) {
            System.err.println("Error occurred while sending SOAP Request to Server");
            e.printStackTrace();
        }
    }
    /**
     * Method used to print the SOAP Response
     */
    private static void printSOAPResponse(SOAPMessage soapResponse) throws Exception {
    	StringWriter sw = new StringWriter();
        TransformerFactory transformerFactory = TransformerFactory.newInstance();
        Transformer transformer = transformerFactory.newTransformer();
        Source sourceContent = soapResponse.getSOAPPart().getContent();
        System.out.print("\nResponse SOAP Message = ");
        StreamResult result = new StreamResult(sw);
        transformer.transform(sourceContent, result);
        System.out.println("Here is another "+sw.toString());
        String resultResponse= sw.toString();
        System.out.println("Result");
        printResult(resultResponse);
        
    }
 
  //for Login	
	public static SOAPMessage buildLogin() throws SOAPException, IOException{
		 MessageFactory messageFactory = MessageFactory.newInstance();
		    SOAPMessage soapMessage = messageFactory.createMessage();

		    SOAPPart soapPart = soapMessage.getSOAPPart();


		    // SOAP Envelope
		    SOAPEnvelope envelope = soapPart.getEnvelope();
		    envelope.addNamespaceDeclaration("xsi", "http://www.w3.org/2001/XMLSchema-instance");
		    envelope.addNamespaceDeclaration("xsd", "http://www.w3.org/2001/XMLSchema");

		        // SOAP Body
		    SOAPBody soapBody = envelope.getBody();
		    //--
			SOAPElement SmsTextFs = soapBody.addChildElement("BulkLogin", "", "http://www.bdmitech.com/m2b");

			SOAPElement name = SmsTextFs.addChildElement("Name");
			SOAPElement password = SmsTextFs.addChildElement("Password");
			name.addTextNode("_name_from_provider_");
			password.addTextNode("_password_from_provider_");

		    MimeHeaders headers = soapMessage.getMimeHeaders();
		    headers.addHeader("SOAPAction","http://www.bdmitech.com/m2b/BulkLogin");

		    soapMessage.saveChanges();
		  
		    soapMessage.writeTo(System.out);
		    return soapMessage;
	}
	
	
	public static SOAPMessage buildSoapMessageTextFs() throws SOAPException, IOException{
		 MessageFactory messageFactory = MessageFactory.newInstance();
		    SOAPMessage soapMessage = messageFactory.createMessage();

		    SOAPPart soapPart = soapMessage.getSOAPPart();
		    SOAPEnvelope envelope = soapPart.getEnvelope();
		    envelope.addNamespaceDeclaration("xsi", "http://www.w3.org/2001/XMLSchema-instance");
		    envelope.addNamespaceDeclaration("xsd", "http://www.w3.org/2001/XMLSchema");
		    SOAPBody soapBody = envelope.getBody();
			SOAPElement SmsTextFs = soapBody.addChildElement("SMS_TXTFS", "", "http://www.bdmitech.com/m2b");

			SOAPElement sender = SmsTextFs.addChildElement("Sender");
			SOAPElement recipient = SmsTextFs.addChildElement("Recipient_Mobile_No");
			SOAPElement message = SmsTextFs.addChildElement("Message");
			SOAPElement isMasked = SmsTextFs.addChildElement("IS_Sender_Masked");
			SOAPElement isSingle = SmsTextFs.addChildElement("IS_SMS_Single");
			SOAPElement accountId = SmsTextFs.addChildElement("Account_ID");
			SOAPElement userName = SmsTextFs.addChildElement("User_Name");
			SOAPElement password = SmsTextFs.addChildElement("Password");
			
			
			sender.addTextNode("__desired_name_");
			recipient.addTextNode("__desired_number_");
			message.addTextNode("__desired_message_");
			isMasked.addTextNode("Y");
			isSingle.addTextNode("Y");
			accountId.addTextNode("__provided_a/c_id_");
			userName.addTextNode("__provided_name_");
			password.addTextNode("__provided_password_");

		    MimeHeaders headers = soapMessage.getMimeHeaders();
		    headers.addHeader("SOAPAction","http://www.bdmitech.com/m2b/SMS_TXTFS");

		    soapMessage.saveChanges();
		    
		    soapMessage.writeTo(System.out);
		    return soapMessage;
	}
	
	public static void printResult(String result) throws SOAPException, IOException{
		String xmlInput = result;

	    MessageFactory factory = MessageFactory.newInstance();
	    SOAPMessage message = factory.createMessage(
	            new MimeHeaders(),
	            new ByteArrayInputStream(xmlInput.getBytes(Charset
	                    .forName("UTF-8"))));

	    SOAPBody body = message.getSOAPBody();

//	    NodeList returnList = body.getElementsByTagName("BulkLoginResult");
//
	    boolean isSuccess = true;
//if you want to put logic before sending message put it here.
//	    for (int k = 0; k < returnList.getLength(); k++) {
//	        NodeList innerResultList = returnList.item(k).getChildNodes();
//	        for (int l = 0; l < innerResultList.getLength(); l++) {
//	            if (innerResultList.item(l).getNodeName()
//	                    .equalsIgnoreCase("web:RETURNCODE")) {
//	                isSuccess = Integer.valueOf(innerResultList.item(l)
//	                        .getTextContent().trim()) == 100 ? true : false;
//	            }
//	        }
//	    }
	    if (isSuccess) {
	        NodeList list = body.getElementsByTagName("SMS_TXTFSResult");

	        for (int i = 0; i < list.getLength(); i++) {
	            NodeList innerList = list.item(i).getChildNodes();

	            for (int j = 0; j < innerList.getLength(); j++) {
	                System.out.println(innerList.item(j).getNodeName());
	                System.out.println(innerList.item(j).getTextContent());
	            }
	        }
	    }
	}
	
}
