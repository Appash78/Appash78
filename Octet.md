package Oct;
import java.io.*;

import java.sql.SQLOutput;

import javax.swing.JFrame;



	public class Octet extends JFrame {
		 
	
	
	    public static void writeInt(int values, OutputStream sortie, int tailleOctet) throws Exception {
	    	
	    		
	        int badValues1 = powerFunction(2, (tailleOctet*8));
	      
	        
	        
	        //Condition pour taille Octet inférieur a 1 ou supérieur à 4
	        if(tailleOctet<1) {
	        	throw new Exception("Erreur: La taille de l'octet doit être compris entre 1 et 4 ! Ici: " + tailleOctet);
	        }
	        else if(tailleOctet>4) {
	        	throw new Exception("Erreur: La taille de l'octet doit être compris entre 1 et 4 ! Ici : " + tailleOctet);
	        }
	        else {
	        	System.out.println("Taille octet bonne\n ");
	        }
	        
	        
	        if(values>=badValues1){

	            throw new Exception("Erreur: valeur trop grande pour "+ tailleOctet +" octet!");

	        } else if (values<0) {

	            throw new Exception("Erreur: Valeur < 0");

	        } else{

	            System.out.println("Valeur juste \n");

	        }

	        byte b1 = (byte) (values & 0xFF); //

	        byte b2 = (byte) (values>>8 & 0xFF);

	        byte b3 = (byte) (values>>16 & 0xFF);

	        byte b4 = (byte) (values>>24 & 0xFF);

	        if(tailleOctet == 1 ) {
	            sortie.write(b1);
	        }
	        else if(tailleOctet == 2) {
	            sortie.write(b2);
	            sortie.write(b1);
	        }
	        else if (tailleOctet == 3) {
	            sortie.write(b3);
	            sortie.write(b2);
	            sortie.write(b1);
	        }
	        else if (tailleOctet == 4) {
	            sortie.write(b4);
	            sortie.write(b3);
	            sortie.write(b2);
	            sortie.write(b1);
	        }
	        else {
	            System.err.println("Taille invalide\n");
	        }
	        
	       
	        
	    }
	    
	   
	    static  int powerFunction(int base, int exponent){ //Méthode pour la puissance
	        int result = 1;
	        for(int i = 0; i < exponent;i++){
	            result= base * result;
	        }
	        return result;
	    }
	    
	     
	    public static void main(String[] args) throws Exception {
	    	
	      
	    	boolean oui = true;
	    	boolean non = false;
	    	
	    	//Instancie la class Scanner en indiquant par le constructeur le flux de données issu du clavier
	    	java.util.Scanner entre = new java.util.Scanner(System.in);
	    	
	    	
	    	System.out.println("Donner votre valeur :");
	    	int values = entre.nextInt(); // Donnée doit correspondre à un entier. Sinon renvoie une Exception
	    	
	    	System.out.println("Donner votre taille d'octet :");
	    	int tailleOctet = entre.nextInt();
	    	
	    	System.out.println("Changer valeur et taille Octet ?\n");
	    	oui = entre.nextBoolean();
	    	if(oui) {
	    		System.out.println("Nouvelle Valeur : \n");
	    		values = entre.nextInt();
	    		System.out.println("Nouvelle TailleOctet : \n");
	    		tailleOctet = entre.nextInt();
	    		System.out.println("Création fichier avec valeur sous le nombre d'octet demandé.\n");
	    		
	    	}
	    	else {
	    		System.out.println("Création fichier avec valeur sous le nombre d'octet demandé.\n");
	    		
	    	}
		    //Création du fichier Bin.txt	
	        FileOutputStream sortie = new FileOutputStream("C:\\Users\\lulub\\Desktop\\Bin.txt");
	        //Ecriture des valeurs dans le fichier de sortie ainsi que la taille d'octet
	        writeInt(values, sortie, tailleOctet);
	        //Fermeture de l'ecriture (fichier)
	        sortie.close();
	        
	        
	        
	    }

	


}

