
public class BlackJack {
	
	public static int kartenFarbe(int zahl){
		return zahl/13;
	}
	
	public static void kartenBezeichnung(int zahl, Karten karte){
		if(zahl <= 13){
			karte.setBezeichnung("HERZ");
		}
		if(zahl > 13 || zahl <= 26){
			karte.setBezeichnung("PIK");
		}
		if(zahl > 26 || zahl <= 39){
			karte.setBezeichnung("KARO");
		}
		if(zahl > 39 || zahl <= 52){
			karte.setBezeichnung("KREUZ");
		}
	}
	
	public static void main(String[] args) 
	{
	    int[] deckarray = new int[312]; //Array für das Deck,für alle Spielerkarten, 6*52 Karten
		Hand croupier = new Hand();
		Hand spieler1 = new Hand();
		Hand spieler2 = new Hand();
		Hand spieler3 = new Hand();
		Karten karte = new Karten();
		
		kartenFarbe(zahl);
		kartenBezeichnung(zahl, karte);
		
		int[]handKarten = new int[21];
		
		
		croupier.kartenZiehen(3, 312);
		spieler1.kartenZiehen(2, 312);
		spieler2.kartenZiehen(5, 312);
		spieler3.kartenZiehen(2, 312);
		
	}

}
