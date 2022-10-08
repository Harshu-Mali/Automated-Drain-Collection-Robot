# Automated-Drain-Collection-Robot
Automated Drain Collection Robot using Microcontroller
#include<reg51.h>

sbit m1=P2^0;
sbit m2=P2^1; //1	//  1
sbit n1=P2^2;  sbit n2=P2^3;  //2 sbit relay=P2^4;

void serial_init(void)
{
TMOD = 0x20; SCON = 0x50;
TH1 = -0x03; //0xFD; TL1 = -0x03;//0xFD; TR1 = 1;
// EA = ES = 1;

}

void main(void)
{
unsigned char mybyte; serial_init();
P2=0x00;
while(1)
{
while(RI==0);	//wait to receive mybyte=SBUF;	//save value RI=0;

if(mybyte=='0')
{


 
m1=0;
 

m2=1;	//1 n1=0;
n2=1; //2
 


}

if(mybyte=='1')	//ok
{


 
m1=1;




}
 

m2=0;	//1 n1=1;
n2=0; //2
 
if(mybyte=='2')	//ok
{
 
m1=1;




}
 

m2=0;	//1 n1=0;
n2=1; //2
 
// fwd-1, rev-5, stop-4, left-2, right-3, spray on -6, off-7.

if(mybyte=='3')
{
m1=1;
m2=0;	//1 m1=0; m2=1; n1=1;
n2=0; //2
 
}
if(mybyte=='4')//ok
{
 
m1=1;





}
 

m2=1;	//1 n1=1;
n2=1; //2 relay=0;
 
if(mybyte=='5')
{
relay=1;


}
}
}
