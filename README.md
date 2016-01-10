# PokerGame
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;


public class Poker {


	public static int[] zufallszahlenErzeugen(int[]kartenarray){
		for(int i=0; i<kartenarray.length;i++){
			int zufzahl = (int)(Math.random()*(kartenarray.length));
			kartenarray[i] = zufzahl;
			System.out.print(kartenarray[i] + ", ");
		}
		return kartenarray;
	}
	
	public static int [] erzeugeHand(int[] handKarten, int[]kartenarray ) {
		int [] hand = new int[5]; 	
		for (int i=0; i<handKarten.length;i++) {
			int zufZahl = (int)(Math.random()*(kartenarray.length-i));
			hand[i] = kartenarray[zufZahl]; 
			int andereStelle = kartenarray[kartenarray.length-i-1];
			kartenarray[kartenarray.length-i-1] = kartenarray[zufZahl];
			kartenarray[zufZahl] = andereStelle;
			System.out.print(hand[i] + " ");
		}
		return hand; 
	}	
	
	public static String farbeFinden(int[]hand){
		String farbe = null ;
		String kartenArt = null;
		for(int i=0; i<hand.length;i++){
			if(hand[i] < 27){
				farbe = "Rot";
			}else{
				farbe = "Schwarz";
			}
			if(hand[i] %13 == 0){
				kartenArt = "HERZ";
			}
			if(hand[i] %13 == 1){
				kartenArt = "PIK";
			}
			else if(hand[i] %13 == 2){
				kartenArt = "KARO";
			}
			else if(hand[i] %13 == 3){
				kartenArt = "KREUZ";
		}
		}
		return kartenArt + " " + farbe;
	}
	
	public static boolean pruefePaare(int[]hand){
		int paare = 0;
		for(int i = 0; i<hand.length;i++){
			for(int j = i+1; j<hand.length;j++){
				if(hand[i]%13 == hand[j]){
					paare++;
				}System.out.println(hand[i] + " ");
			}
		}
		if(paare == 2){
			return true;
		}System.out.println("Zwei Paare: " + paare);
		
		if(paare == 3){
			return true;
		}System.out.println("Drillinge: " + paare);
		
//		int anz = 0;
//		for(int i=0; i<hand.length;i++){
//			for(int j=i+1; j<hand.length;j++){
//				if(farbe(hand[i])== farbe(hand[j])){
//					anz++;
//				}
//			}
//			if(anz == 4){
//			return true;
//		    }System.out.print("Anzahl Flush: " + anz);
//		}
		return false;
	}
	
	
	public static void main(String[] args) 
	{
//		int[]kartenarray = new int[52];
//		System.out.println("Kartenarray: ");
//		zufallszahlenErzeugen(kartenarray);
//		int[] handKarten = new int[5];
//		System.out.println();
//		System.out.println();
//		System.out.println("Hand: ");
//		erzeugeHand(handKarten, kartenarray);
//		farbeFinden(handKarten);
//		System.out.println();
//		System.out.println();
//		System.out.println();
//		pruefePaare(handKarten);
		
		Connection c = null;
	    try {
	      Class.forName("org.sqlite.JDBC");
	      c = DriverManager.getConnection("jdbc:sqlite:poker.db");
	    } catch ( Exception e ) {
	      System.err.println( e.getClass().getName() + ": " + e.getMessage() );
	      System.exit(0);
	    }
	    System.out.println("Opened database successfully");
	    
	    Statement stmt = null;
	    try {
	      Class.forName("org.sqlite.JDBC");
	      c = DriverManager.getConnection("jdbc:sqlite:test.db");
	      System.out.println("Opened database successfully");

	      stmt = c.createStatement();
	      String sql = "CREATE TABLE Poker IF NOT EXISTS " +
	                   "(UNIXTIMESTAMP LONG NOT NULL," +
	                   " AnzahlDerLäufe INT NOT NULL, " + 
	                   " EinPaar INT NOT NULL, " + 
	                   " ZweiPaare INT NOT NULL" + 
	                   " Drilling INT NOT NULL" + 
	                   " RoyalFlush INT NOT NULL" + 
	                   " Straight INT NOT NULL" + 
	                   " Poker INT NOT NULL" + 
	                   " )"; 
	      stmt.executeUpdate(sql);
	      stmt.close();
	      c.close();
	    } catch ( Exception e ) {
	      System.err.println( e.getClass().getName() + ": " + e.getMessage() );
	      System.exit(0);
	    }
	    System.out.println("Table created successfully");
	    
	   
	    
	    
	    
	    
	}

}
