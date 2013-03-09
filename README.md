This-one
========

import java.applet.*; import java.awt.*; import java.awt.event.*; import java.util.*; import java.lang.*; import javax.swing.*; import java.awt.geom.*; public class HangMan extends JApplet implements ActionListener {          public static void main(String[] args){     	JFrame frame =new JFrame();         frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);         frame.setTitle("Hangman");         frame.setLocation(300,50);         HangMan applet = new HangMan();         applet.init();         frame.getContentPane().add(applet);         frame.pack();          frame.setVisible(true);    }                static final int MAX=10; 	// max number of trying till loss       public int errors;			//amount of error trial       public String msg;			// to show a message to the user        public String ranWord;	    // get a random word in it       public StringBuffer gWord;   // gussed word       public JToggleButton A;	       public JToggleButton B;       public JButton C;       public JButton D;       public JButton E;    //..... rest of the letters                    public Font font= new Font("Monospaced",Font.BOLD,16);       HMpanel panel = new HMpanel();     public void init(){     	JPanel p = new JPanel();     	JPanel m = new JPanel();     	p.setLayout(new GridLayout(3,10,0,1));     	 A = new JToggleButton("A"); 		p.add(A);     	 B = new JToggleButton("B");		p.add(B);     	 C = new JButton ("C");				p.add(C);     	 D = new JButton ("D");				p.add(D);     	 E = new JButton ("E");				p.add(E);    	 // ... the rest     	  	     	  A.addActionListener(this);     	  B.addActionListener(this);     	  C.addActionListener(this);     	  D.addActionListener(this);     	  E.addActionListener(this);     	  // ...    	     	JMenuBar menubar =new JMenuBar();     	JMenu gameMenu =new JMenu("Game");     	JMenuItem restart =new JMenuItem("Restart");     	JMenuItem help =new JMenuItem("Help");     	JMenuItem about =new JMenuItem("About");     	JMenuItem quit =new JMenuItem("Quit");     	     	menubar.add(gameMenu);     	gameMenu.add(restart);     	gameMenu.addSeparator();     	gameMenu.add(help);     	gameMenu.add(about);     	gameMenu.addSeparator();     	gameMenu.add(quit);     	     	restart.addActionListener(this);     	help.addActionListener(this);     	about.addActionListener(this);     	quit.addActionListener(this);     	m.setLayout(new BorderLayout());     	m.add(menubar,BorderLayout.WEST);     	     	this.getContentPane().setLayout(new BorderLayout());     	this.getContentPane().add(p,BorderLayout.SOUTH);     	this.getContentPane().add(m,BorderLayout.NORTH);     	this.getContentPane().add(panel,BorderLayout.CENTER);     	     	initGame();     }          public void initGame(){       	errors=0;       	       	msg=new String("you have NO mistakes..Good Luck");         String [] str={"computer","calculator"};                                                Random ran = new Random();                        int intRan = (int) (Math.floor(Math.random()*(str.length-0+1))+1);                        ranWord= new String(str[intRan]);                        System.out.println(ranWord);                        char pos[]=new char[ranWord.length()];                        for(int i= 0; i &lt;ranword.length()>                           {pos[i]='*'; }                          String s= new String(pos);                       gWord= new StringBuffer(s);                                                       }                              public void actionPerformed (ActionEvent e){      	     String action = e.getActionCommand();      	     char EL ;  			//entered letter              if (action.equals("A")) {                        	EL = 'a';                        	entLetter(EL);                        	A.setEnabled(false); 		                        	}            	if (action.equals("B")) {                        	EL = 'b';                        	entLetter(EL);                        	B.setEnabled(false);}                      	             if(action.equals("C")){             	        EL='c';             	        entLetter(EL);             	       C.setEnabled(false);}           	                     if (action.equals("D")) {                        	EL = 'd';                        	entLetter(EL);                        	D.setEnabled(false);}            if (action.equals("E")) {                        	EL = 'e';                        	entLetter(EL);                        	E.setEnabled(false);}             // ....                       		                        		                      JFrame fmsg = new JFrame();                      fmsg.setBackground(Color.WHITE);                      JTextArea ta = new JTextArea();                      ta.setRows(7);                      ta.setEditable(false);                      fmsg.setLocation(500,300);                                              		           	             if (action.equals("Help")) {                   fmsg.setTitle("HELP");                   String textToApper = "To win the hangman you must correctly guess the letters of the hidden word.";             	  ta.append(textToApper);             	  fmsg.getContentPane().add(ta);             	  fmsg.pack();             	  fmsg.setVisible(true);                    }                     	            if (action.equals("About")) {                  fmsg.setTitle("About Hang-Man");                   String textToApper = "developed by:" + ta.append(textToApper);             	  fmsg.getContentPane().add(ta);             	  fmsg.pack();             	  fmsg.setVisible(true);                    }              if (action.equals("Quit")) {                  System.exit(0);                    }                                if (action.equals("Restart")) {                  int response = JOptionPane.showConfirmDialog(null,                  "Are You Sure You Want To Restart", "Restart", 1, -1);            switch(response) {               case JOptionPane.YES_OPTION:                 restartGame();              break;              case JOptionPane.NO_OPTION: break;              case JOptionPane.CANCEL_OPTION: break;               case JOptionPane.CLOSED_OPTION: break;          }      }       }                public void restartGame()          {          	A.setEnabled(true);	 		A.setSelected(false);          	B.setEnabled(true);			B.setSelected(false);          	C.setEnabled(true);			C.setSelected(false);          	D.setEnabled(true);          	E.setSelected(false);          	init();          }   	          	                        	                                         	                                                private void entLetter(char en)		       	{  	if(ranWord.indexOf(en)==-1){                        		msg="";                        		errors++;	                        	    msg="you  have "+errors+" mistake/s";}                        	                 		if(errors==MAX){                        		msg=" You Lose.. Better Luck Next Time";                          	return;                          	}                    		for (int i=0;i&lt;ranword.length();i++){>                        	if(ranWord.charAt(i)==en){                        		gWord.setCharAt(i,en);                        		System.out.println(gWord);                        	}}                        	                        	                        String s=new String (gWord);                                                if(s.indexOf('*')==-1){                        	msg="Congrats,You Win";                        	return;                        }}                                    	     class HMpanel extends JPanel{   	public HMpanel(){   		   		setPreferredSize(new Dimension(800,500));   		setBackground(Color.white);   			}   	   	public void paintComponent(Graphics g){   		super.paintComponent(g);   		Graphics2D g2 = (Graphics2D)g;   		   		Stroke stroke = new BasicStroke(5,BasicStroke.CAP_ROUND,BasicStroke.JOIN_MITER);   		g2.setStroke(stroke);   		   		Ellipse2D elp=new Ellipse2D.Double(530,250,40,35);   		Line2D line1 = new Line2D.Double(380,450,700,450);	   		// ... the drawing  		   		   		repaint();   		   		if(errors>0)   			{g2.setColor(new Color(153,204,0));	   			 g2.draw(line1);}	   		if(errors>1)   			{g2.setColor(new Color(99,44,3));	   			 g2.draw(line2);}		   		if(errors>2)   			{g2.draw(line3);}	   		if(errors>3)   			{g2.setColor(new Color(255,153,0));	   			 g2.draw(line4);}		   		if(errors>4)   			{g2.setColor(Color.black);   			 g2.draw(elp);}	   		if(errors>5)   			{g2.draw(line5);}		   		if(errors>6)   			{g2.draw(line6);}								   		if(errors>7)   		{g2.draw(line7);}   		if(errors>8)   		{g2.draw(line8);}   		if(errors>9)   		{g2.draw(line9);}	   		   		//show msg   		setFont(font);   		g2.setColor(new Color(0,102,153));  		g2.drawString(msg,30,275);  		g2.setColor(Color.black);   		g2.drawString(new String(gWord),110,80);   	   		   	}}}