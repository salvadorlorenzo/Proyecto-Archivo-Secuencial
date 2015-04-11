# Proyecto-Archivo-Secuencial
#include <stdio.h> 
#include <string>
#include <conio.h> 
#include <iostream> 
#include <ctype.h>
#include <cstring>

using namespace std;

int main(){
	struct tipo_registro{
		int codigo;
		char nombre[20];
		char caracteristica[60];
		int precio;
	}registro;
	int opc;
	int codigo;
	FILE *arch;
	
	do{
		   cout<<"-----BIENVENIDO-----";
           cout<<"\n 1.INGRESAR UN REGISTRO";
           cout<<"\n 2.CONSULTAR UN REGISTRO";
           cout<<"\n 3.MODIFICAR UN REGISTRO";
           cout<<"\n 4.ELIMINAR UN REGRISTRO";
           cout<<"\n 5.SALIR DEL PROGRAMA";
           cout<<"\n QUE DESEA REALIZAR?\t\n";cin>>opc;
           
           switch(opc){
           	case 1:{
           		cout << "\n\rINGRESAR UN REGISTRO";
				arch=fopen("Data_base","rb+");	
				if(arch==NULL)
				arch=fopen("Data_base","wb");	

				cout << "\n\n\n\rCodigo del registro: "; cin >> codigo;
				fread(&registro,sizeof(registro),1,arch);

				while(!feof(arch))
				{
				if(registro.codigo==codigo)
				{
				cout << "\n\n\n\rRegistro duplicado !!!";
				fclose(arch);
				getch();
				}
				fread(&registro,sizeof(registro),1,arch);
				}
				cout << "\n\rNombre : "; cin>> registro.nombre;
				cout << "\n\rCaracteristica : "; cin >> registro.caracteristica;
				cout << "\n\rPrecio : "; cin >> registro.precio;
				
				cout << "\n\n\n\rRegistro guardado";
				cout << "\n\r<<< Oprima cualquier tecla para continuar >>>";
				getch();
				   break;
			   }    
								                                             
            case 2:{
            	cout << "\n\rCONSULTA DE REGISTROS";
				arch=fopen("Data_base","rb");
				
				if(arch==NULL)
				{
				cout << "\n\n\n\rNo existe el archivo !!!";
				cout << "\n\r<<< Oprima cualquier tecla para continuar >>>";
				getch();
				}
				cout << "\n\n\n\rCodigo del registro: "; cin >> codigo;
				fread(&registro,sizeof(registro),1,arch);
				while(!feof(arch))
				{
				if(codigo==registro.codigo)
				{
				cout << "\n\rCodigo-----Nombre-----Caracteristica-----Precio"; 
				cout << "\n\r------------------------------------------------------";
				printf("\n\r%3d\t%30s\t%3d\t\t$%4.2f\t%c",registro.codigo,registro.nombre,registro.caracteristica,registro.precio);
				fclose(arch);
				cout << "\n\r<<< Oprima cualquier tecla para continuar >>>";
				getch();
				}
				fread(&registro,sizeof(registro),1,arch);
				}
				cout << "\n\rNo se encuentra ese registro !!!";
				fclose(arch);
				cout << "\n\r<<< Oprima cualquier tecla para continuar >>>";
				getch();
				break;
			}
            case 3:{
            	cout << "\n\rMODIFICACION DE REGISTROS DE PRODUCTOS";
				arch=fopen("Data_base","rb+");
				
				if(arch==NULL)
				{
				cout << "\n\n\n\rNo existe el archivo !!!";
				cout << "\n\r<<< Oprima cualquier tecla para continuar >>>";
				getch();
				}
				cout << "\n\n\n\rCodigo del registro: "; cin >> codigo;
				fread(&registro,sizeof(registro),1,arch);
			
				while(!feof(arch)) 
				
				{
				if(codigo==registro.codigo)
				{
				cout << "\n\rCodigo-----Nombre-----Caracteristica-----Precio"; 
				cout << "\n\r------------------------------------------------------";
				printf("\n\r%3d\t%30s\t%3d\t\t$%4.2f\t%c",registro.codigo,registro.nombre,registro.caracteristica,registro.precio);
				
				cout << "\n\n\n\rAnote los nuevos datos ...";
				cout << "\n\rNombre: "; cin >> registro.nombre;
				cout << "\n\rCaracteristica : "; cin >> registro.caracteristica;
				cout << "\n\rPrecio : "; cin >> registro.precio;
				
				fseek(arch,ftell(arch)-sizeof(registro),SEEK_SET);
				fwrite(&registro,sizeof(registro),1,arch);
				
				fclose(arch); 
				cout << "\n\n\n\rRegistro modificado !!!";
				cout << "\n\r<<< Oprima cualquier tecla para continuar >>>";
				getch();
				}
				fread(&registro,sizeof(registro),1,arch);
				}
				cout << "\n\rNo se encuentra ese registro !!!";
				fclose(arch);
				cout << "\n\r<<< Oprima cualquier tecla para continuar >>>";
				getch();
				
				break;
			}
			
			case 4:{
				cout << "\n\rELIMINACION DE REGISTROS";
				arch=fopen("Data_base","rb+"); 
	
				if(arch==NULL) 
				{
				cout << "\n\n\n\rNo existe el archivo !!!";
				cout << "\n\r<<< Oprima cualquier tecla para continuar >>>";
				getch();
				}
				cout << "\n\n\n\rCodigo del registro: "; cin >> codigo;
				fread(&registro,sizeof(registro),1,arch);
				
				while(!feof(arch))
				{
				if(codigo==registro.codigo)
				{
				cout << "\n\rCodigo-----Nombre-----Caracteristica-----Precio"; 
				cout << "\n\r------------------------------------------------------";
				printf("\n\r%3d\t%30s\t%3d\t\t$%4.2f\t%c",registro.codigo,registro.nombre,registro.caracteristica,registro.precio);
					
				registro.codigo=0;
				strcpy(registro.nombre,"");
				strcpy(registro.caracteristica,"");
				registro.precio=0;
	
				fseek(arch,ftell(arch)-sizeof(registro),SEEK_SET);
				fwrite(&registro,sizeof(registro),1,arch);
		
				cout << "\n\n\n\rRegistro eliminado !!!";
				}
				fclose(arch);
				cout << "\n\r<<< Oprima cualquier tecla para continuar >>>";
				getch();
				}
				fread(&registro,sizeof(registro),1,arch);
				}
				cout << "\n\rNo se encuentra ese registro !!!";
				fclose(arch);
				cout << "\n\r<<< Oprima cualquier tecla para continuar >>>";
				getch();
				
				break;
			
			case 5:exit(0);
			}
            
            		  	   
		   }

		while(opc!=5);
		
		return (0);

}
