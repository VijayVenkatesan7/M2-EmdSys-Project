# CODE USED FOR OVERALL AND LED PROCESS:
#include<pic.h>
__CONFIG(0X3F32);
#include"lcd.h"
#include"pic_serial.h"
#define Relay RB0
#define set RB1
#define mov RB2
#define inc RB3
#define dec RB4
#define ent RB5
#define Limit RC0
#define Alarm RC1
signed char count=0;
unsigned char rc=0,data_rcv[80],i=0,fp_id=0,fpid1=0,chk_sum=0,va=0,k=0,kk,ct;
unsigned int j,x0,x1,x2;
void display(unsigned char val);
void fpid(unsigned char val);
void result();
void ent_fpid();
unsigned char fingerVerifySuccess=0;
unsigned char RelayAlarm=0;
void interrupt serRx()
{
if(RCIF)
 {
	data_rcv[rc]=RCREG;
	rc++;
    RCIF=0;
 }
}

void main()
{
TRISB=0x00;
PORTB=0xFF;
TRISD=0x00;
TRISC=0x81;
Limit=1;
Alarm=0;
Relay=0;
Delay(200);
Lcd_Init();
Serial_Init(57600);
Lcd_Display(0x80,"VEHICLE SECURITY");
Lcd_Display(0xC0,"     SYSTEM     ");
Delay(65000); Delay(65000);
Receive(1);
Lcd_data(0x01,0);
Delay(65000); 
	while(1)
	{

	   if(!inc){while(!inc);count++;if(count>4){count=0;}}
	   if(!dec){while(!dec);count--;if(count<0){count=4;}}
	   if(!ent){while(!ent);fpid(count);}
	   display(count);
	

		if(fingerVerifySuccess==1)
			{
				if(Limit==0)
					{
						Relay=1;
					}
					else
						{
							Alarm=1;
						}
				fingerVerifySuccess=0;
				RelayAlarm=1;
			}
		if(!mov){while(!mov);Alarm=0;Relay=0;RelayAlarm=0;}
		if(RelayAlarm==1){ if(Limit==1){Alarm=1;Relay=0;}else{Alarm=0;Relay=1;} }
	}
}

void display(unsigned char val)
{
switch(val)
{
case 1:
Lcd_Display(0xC0,"ENROLLEMENT     ");
   break;
   case 2:
Lcd_Display(0xC0,"IDENTIFY FP     ");
   break;
   case 3:
Lcd_Display(0xC0,"DEL USR FP      ");
   break;
   case 4:
Lcd_Display(0xC0,"DEL ALL FP      ");
   break;
 default:
Lcd_Display(0x80,"select option   ");
Lcd_Display(0xC0,"                ");
   break;
}
}

void fpid(unsigned char val)
{
	Lcd_data(0x01,0);
	for(rc=0;rc<50;rc++)data_rcv[rc]=0;
	rc=0;

	switch(val)
	{
		  case 1:		
			ent_fpid();
	Serial_Conout("\xEF\x01\xFF\xFF\xFF\xFF\x01\x00\x03\x01\x00\x05",12);
			Delay(65000);Delay(65000);
	Serial_Conout("\xEF\x01\xFF\xFF\xFF\xFF\x01\x00\x04\x02\x01\x00\x08",13);
			Delay(65000);Delay(65000);
			Serial_Conout("\xEF\x01\xFF\xFF\xFF\xFF\x01\x00\x03\x01\x00\x05",12);
			Delay(65000);Delay(65000);	
			Serial_Conout("\xEF\x01\xFF\xFF\xFF\xFF\x01\x00\x04\x02\x02\x00\x09",13);
			Delay(65000);Delay(65000);
			Serial_Conout("\xEF\x01\xFF\xFF\xFF\xFF\x01\x00\x03\x05\x00\x09",12);
			Delay(5000); Delay(65000);
			Serial_Conout("\xEF\x01\xFF\xFF\xFF\xFF\x01\x00\x06\x06\x02",11);
			Serial_Out(0);
			Serial_Out(fp_id);
			chk_sum=fp_id+15;
			Serial_Out(0);
			Serial_Out(chk_sum);
			Delay(65000);Delay(65000);
			i=1;
			result();
			break;
case 2:		
		Lcd_Display(0xc0,"--Processing.---");	
		Serial_Conout("\xEF\x01\xFF\xFF\xFF\xFF\x01\x00\x03\x01\x00\x05",12);  
		Delay(65000);Delay(65000);
		Serial_Conout("\xEF\x01\xFF\xFF\xFF\xFF\x01\x00\x04\x02\x01\x00\x08",13);
		Delay(65000);Delay(65000);
		Serial_Conout("\xEF\x01\xFF\xFF\xFF\xFF\x01\x00\x08\x1b\x01\x00\x00\x01\x01\x00\x27",17);	
		Delay(65000);Delay(65000);
		i=2;
		result();
		break;
		case 3:	
		ent_fpid();	
		Serial_Conout("\xEF\x01\xFF\xFF\xFF\xFF\x01\x00\x07\x0C",10);
		Delay(65000);Delay(65000);
		Serial_Out(0);
		Delay(65000);Delay(65000);
		Serial_Out(fp_id);
		Serial_Out(0);
		Serial_Out(0x01);
		chk_sum=fp_id+21;
		Serial_Out(0);
		Serial_Out(chk_sum);Delay(65000);Delay(65000);
		i=3;
		result();	
		break;
		case 4:
		Lcd_Display(0xc0,"--Processing.---");
		Serial_Conout("\xEF\x01\xFF\xFF\xFF\xFF\x01\x00\x03\x0D\x00\x11",12);
		Delay(65000);Delay(65000);
		i=4;
		result();			
		break;	
		default:	
		break; 
	}
}
void ent_fpid()
{
	while(!ent);Delay(65000);
	Lcd_Display(0x80,"Enter ID No: 000");
	fp_id=0;		
	while(ent)
	{
		if(!inc){while(!inc);fp_id++;if(fp_id>=255)fp_id=0;Lcd_Decimal(0x8D,fp_id,3);}
		if(!dec){while(!dec);fp_id--;if(fp_id>=255)fp_id=255;Lcd_Decimal(0x8D,fp_id,3);}
	}
	Lcd_Display(0xc0,"--Processing.---");
	ct++;					
}
void result()
{	
		Lcd_data(0x01,0);		
	  if(i==1)
	  {
				if((data_rcv[69]==0x00)&&(rc>70))
				{
				Lcd_Display(0x80," Enrollment     ");
				Lcd_Display(0xC0,"    Success     ");
				}
				else if(data_rcv[69]==0x02)
				{
				Lcd_Display(0x80,"   No Finger    ");
				}
				else
				{
				Lcd_Display(0x80," Enrollment     ");
				Lcd_Display(0xC0,"  Not  Success  ");
				}
				i=0; 
	  }
	  else if(i==2)
	  {
				if(data_rcv[33]==0x00)
				{
				   if(data_rcv[35]==0) {Lcd_Display(0x80,"Keep fng proper "); goto down;}
					Lcd_Display(0x80,"    Success     ");
					Lcd_Display(0xc0," Finger ID:     ");
					Lcd_Decimal(0xcb,data_rcv[35],3);
					Delay(65000);
					fingerVerifySuccess=1;		
				}
				else if(data_rcv[33]==0x09)
				{			
					Lcd_Display(0x80,"Not Find Finger ");
					Delay(65000);
					Alarm=1;Relay=0;
				}
				else if(data_rcv[33]==0x24)
				{
				Lcd_Display(0x80,"Not valid Finger "); 
				Alarm=1;Relay=0;
				} 
				Serial_Init(57600);Receive(1);
				i=0; 
	  }
	  else if(i==3)
	  {
				if(data_rcv[9]==0x00)
				{
					Lcd_Display(0x80,"    Finger Id   ");
					Lcd_Display(0xc0," Deleted        ");
				}
				else if(data_rcv[9]==0x10)
				{
					Lcd_Display(0x80,"Fail To delete  ");
					Lcd_Display(0xc0," Finger Id      ");
				}
				else if(data_rcv[9]==0x01)
				{
					Lcd_Display(0x80,"Receiving       ");
					Lcd_Display(0xc0," Error          ");
				}
				i=0;			
	  }
	  else if(i==4)
	  {
			 if(data_rcv[9]==0x00)
				{
					Lcd_Display(0x80,"  Finger id's   ");
					Lcd_Display(0xc0," Deleted        ");
					kk=0;Delay(65000);
				}
		
				else if(data_rcv[9]==0x11)
				{
					Lcd_Display(0x80,"Fail To delete  ");
					Lcd_Display(0xc0,"Finger Id's     ");
				}
				else if(data_rcv[9]==0x01)
				{
					Lcd_Display(0x80,"Receiving       ");
					Lcd_Display(0xc0," Error          ");
				}
				i=0;	
	 }
				Delay(65000);
				Lcd_data(0x01,0);
				Lcd_Display(0x80,"select option   ");
				Lcd_Display(0xC0,"                ");
				down:;
 }




