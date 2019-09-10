/**
* gZip 형식 압축
* 
* MethodName : GZipComp
* 
* @param String reqJson 압축할 문자열
* @return
*/
static public byte[] GZipComp(String reqJson){
	int length;
	byte[] arrBody = null;

	GZIPOutputStream gos = null;
	ByteArrayOutputStream baos = null;
	ByteArrayInputStream bais = null;
		
	try{
		byte[] buffer = new byte[1024];
			
		baos = new ByteArrayOutputStream();
		gos = new GZIPOutputStream(baos);
		bais = new ByteArrayInputStream(reqJson.getBytes("UTF-8"));
			
		while((length=bais.read(buffer))>0){
			gos.write(buffer,0, length);
		}
			
		bais.close();
			
		gos.flush();
		gos.finish();
		baos.flush();
		
		gos.close();
		baos.close();
		
		arrBody = baos.toByteArray();
		
		System.out.println(new String(Base64.encodeBase64(arrBody)));
		System.out.println("Zip file has been created");
		
	}catch(Exception e){
		e.printStackTrace();
	}finally{
		try{
			if(gos!=null){
				gos.close();
				gos = null;
			}
			if(baos!=null){
				baos.close();
				baos = null;
			}
			if(bais!=null){
				bais.close();
				bais = null;
			}
		}catch(Exception e){
			e.printStackTrace();
		}
	}
		
	return Base64.encodeBase64(arrBody);
}
