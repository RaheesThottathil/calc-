import javax.naming.spi.DirStateFactory.Result;
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.geom.RoundRectangle2D;




public class calc implements ActionListener{


//------------------------------------------------- button shape with by" classss Roundbutton "------------------------------------------------------//
class RoundedButton extends JButton {
      
    private Color normalColor;
    private Color pressedColor;

RoundedButton(String text) {
    super(text);
    setContentAreaFilled(false);
    normalColor = Color.GRAY;
    pressedColor =Color.ORANGE; // turn ornage
    setBackground(normalColor);
    addMouseListener(new java.awt.event.MouseAdapter() { // Add mouse press animation

    @Override
    public void mousePressed(java.awt.event.MouseEvent evt) {
    setBackground(pressedColor);  // darker when pressed
    }

    @Override
    public void mouseReleased(java.awt.event.MouseEvent evt) {
    Timer timer = new Timer(100, new ActionListener() { // Small delay before returning to normal
    public void actionPerformed(ActionEvent e) {
    setBackground(normalColor);
    }
    });
    timer.setRepeats(false);
    timer.start();
    }
    });
    }
    
    @Override
    protected void paintComponent(Graphics g) {
    Graphics2D g2 = (Graphics2D) g.create();
    g2.setColor(getBackground());
    g2.fillRoundRect(0, 0, getWidth(), getHeight(), 20, 20); // 20 = curve 
    super.paintComponent(g);
    g2.dispose();
    }
    
    @Override
    protected void paintBorder(Graphics g) {
    Graphics2D g2 = (Graphics2D) g.create();
    g2.setColor(getForeground());
    g2.drawRoundRect(0, 0, getWidth() - 1, getHeight() - 1, 20, 20);
    g2.dispose();
    }
    }
//-----------------------------------------------------------------------------------------------------------------------//
    
JLabel screen;

RoundedButton sevenButton;
RoundedButton eightButton;
RoundedButton nineButton;
RoundedButton fourButton;
RoundedButton fiveButton;
RoundedButton sixButton;
RoundedButton oneButton;
RoundedButton twoButton;
RoundedButton threeButton;
RoundedButton zeroButton;
RoundedButton dotButton;
RoundedButton clearButton;
RoundedButton percentageButton;
RoundedButton divButton;
RoundedButton mulButton;
RoundedButton minusButton;
RoundedButton plusButton;
RoundedButton equalButton;
RoundedButton deleteButton;

Boolean OperatorClicked=false;
String oldvalue;
String newvalue;
Float oldvalueFloat;
Float newvalueFloat;
Float  Result;
String Operator;

calc() {

        JFrame jf = new JFrame("calculator");
        jf.getContentPane().setBackground(Color.BLACK);
        jf.setSize(330, 450);
        jf.setLayout(null);
        jf.setLocation(500, 150);

        screen = new JLabel();
        screen.setBounds(20, 30, 270, 40);
        screen.setBackground(Color.GRAY);
        screen.setForeground(Color.WHITE);
        screen.setOpaque(true);
        screen.setHorizontalAlignment(SwingConstants.CENTER);
        screen.setFont(new Font("Arial", Font.BOLD, 24));
        jf.add(screen);

        // Now using RoundedButton instead of JButton!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

        clearButton = new RoundedButton("AC");    
        clearButton.setBackground(Color.GRAY);
        clearButton.setForeground(Color.ORANGE);
        clearButton.setBounds(20, 90, 60, 50);
        clearButton.addActionListener(this);
        clearButton.setFont(new Font("Arial", Font.BOLD, 16));
        jf.add(clearButton);

     deleteButton = new RoundedButton("DL"); 
        deleteButton.setBackground(Color.GRAY);
        deleteButton.setForeground(Color.ORANGE);
        deleteButton.setBounds(90, 90, 60, 50);
        deleteButton.addActionListener(this);
        deleteButton.setFont(new Font("Arial", Font.BOLD, 16));
        jf.add(deleteButton);

     percentageButton = new RoundedButton("%");
        percentageButton.setBounds(160, 90, 60, 50);
        percentageButton.setBackground(Color.GRAY);
        percentageButton.setForeground(Color.ORANGE);
        percentageButton.addActionListener(this);
        percentageButton.setFont(new Font("Arial", Font.BOLD, 16));
        jf.add(percentageButton);

        divButton = new RoundedButton("/");
        divButton.setBounds(230, 90, 60, 50);
        divButton.setBackground(Color.GRAY);
        divButton.setForeground(Color.ORANGE);
        divButton.addActionListener(this);
        divButton.setFont(new Font("Arial", Font.BOLD, 16));
        jf.add(divButton);

        // Same for rest buttons
     sevenButton = new RoundedButton("7");
        sevenButton.setBounds(20, 150, 60, 50);
        sevenButton.setBackground(Color.GRAY);
        sevenButton.setForeground(Color.WHITE);
        sevenButton.addActionListener(this);
        sevenButton.setFont(new Font("Arial", Font.BOLD, 16));
        jf.add(sevenButton);

     eightButton = new RoundedButton("8");
        eightButton.setBounds(90, 150, 60, 50);
        eightButton.setBackground(Color.GRAY);
        eightButton.setForeground(Color.WHITE);
        eightButton.addActionListener(this);
        eightButton.setFont(new Font("Arial", Font.BOLD, 16));
        jf.add(eightButton);

     nineButton = new RoundedButton("9");
        nineButton.setBounds(160, 150, 60, 50);
        nineButton.setBackground(Color.GRAY);
        nineButton.setForeground(Color.WHITE);
        nineButton.addActionListener(this);
        nineButton.setFont(new Font("Arial", Font.BOLD, 16));
        jf.add(nineButton);

     mulButton = new RoundedButton("x");
        mulButton.setBounds(230, 150, 60, 50);
        mulButton.setBackground(Color.GRAY);
        mulButton.setForeground(Color.ORANGE);
        mulButton.addActionListener(this);
        mulButton.setFont(new Font("Arial", Font.BOLD, 16));
        jf.add(mulButton);

     fourButton = new RoundedButton("4");
        fourButton.setBounds(20, 210, 60, 50);
        fourButton.setBackground(Color.GRAY);
        fourButton.setForeground(Color.WHITE);
        fourButton.addActionListener(this);
        fourButton.setFont(new Font("Arial", Font.BOLD, 16));
        jf.add(fourButton);

     fiveButton = new RoundedButton("5");
        fiveButton.setBounds(90, 210, 60, 50);
        fiveButton.setBackground(Color.GRAY);
        fiveButton.setForeground(Color.WHITE);
        fiveButton.addActionListener(this);
        fiveButton.setFont(new Font("Arial", Font.BOLD, 16));
        jf.add(fiveButton);

     sixButton = new RoundedButton("6");
        sixButton.setBounds(160, 210, 60, 50);
        sixButton.setBackground(Color.GRAY);
        sixButton.setForeground(Color.WHITE);
        sixButton.addActionListener(this);
        sixButton.setFont(new Font("Arial", Font.BOLD, 16));
        jf.add(sixButton);

     minusButton = new RoundedButton("-");
        minusButton.setBounds(230, 210, 60, 50);
        minusButton.setBackground(Color.GRAY);
        minusButton.setForeground(Color.ORANGE);
        minusButton.addActionListener(this);
        minusButton.setFont(new Font("Arial", Font.BOLD, 16));
        jf.add(minusButton);

     oneButton = new RoundedButton("1");
        oneButton.setBounds(20, 270, 60, 50);
        oneButton.setBackground(Color.GRAY);
        oneButton.setForeground(Color.WHITE);
        oneButton.addActionListener(this);
        oneButton.setFont(new Font("Arial", Font.BOLD, 16));
        jf.add(oneButton);

     twoButton = new RoundedButton("2");
        twoButton.setBounds(90, 270, 60, 50);
        twoButton.setBackground(Color.GRAY);
        twoButton.setForeground(Color.WHITE);
        twoButton.addActionListener(this);
        twoButton.setFont(new Font("Arial", Font.BOLD, 16));
        jf.add(twoButton);

     threeButton = new RoundedButton("3");
        threeButton.setBounds(160, 270, 60, 50);
        threeButton.setBackground(Color.GRAY);
        threeButton.setForeground(Color.WHITE);
        threeButton.addActionListener(this);
        threeButton.setFont(new Font("Arial", Font.BOLD, 16));
        jf.add(threeButton);

     plusButton = new RoundedButton("+");
        plusButton.setBounds(230, 270, 60, 50);
        plusButton.setBackground(Color.GRAY);
        plusButton.setForeground(Color.ORANGE);
        plusButton.addActionListener(this); 
        plusButton.setFont(new Font("Arial", Font.BOLD, 16));
        jf.add(plusButton);

     zeroButton = new RoundedButton("0");
        zeroButton.setBounds(90, 330, 60, 50);
        zeroButton.setBackground(Color.GRAY);
        zeroButton.setForeground(Color.WHITE);
        zeroButton.addActionListener(this);
        zeroButton.setFont(new Font("Arial", Font.BOLD, 16));
        jf.add(zeroButton);

     dotButton = new RoundedButton(".");
        dotButton.setBounds(160, 330, 60, 50);
        dotButton.setBackground(Color.GRAY);
        dotButton.setForeground(Color.WHITE);
        dotButton.addActionListener(this);
        dotButton.setFont(new Font("Arial", Font.BOLD, 16));
        jf.add(dotButton);

     equalButton = new RoundedButton("=");
        equalButton.setBounds(230, 330, 60, 50);
        equalButton.setBackground(Color.ORANGE);
        equalButton.setForeground(Color.WHITE);
        equalButton.addActionListener(this);
        equalButton.setFont(new Font("Arial", Font.BOLD, 16));
        jf.add(equalButton);

        jf.setVisible(true);
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {
        new calc();
    }
@Override
public void actionPerformed(ActionEvent e){
  
    if(e.getSource()== sevenButton){

        if(OperatorClicked){
        screen.setText("7");
        OperatorClicked=false;
        }else{
        screen.setText(screen.getText()+"7");
        }
           
    }else if (e.getSource()== eightButton){

        if(OperatorClicked){
        screen.setText("8");
        OperatorClicked=false;
        }else{
        screen.setText(screen.getText()+"8");
        }

    }else if(e.getSource()== nineButton){

        if(OperatorClicked){
        screen.setText("9");
        OperatorClicked=false;
        }else{
        screen.setText(screen.getText()+"9");
        }

    }else if(e.getSource()== fourButton){
       
        if (OperatorClicked) {
        screen.setText("4");
        OperatorClicked=false;   
        }else{
        screen.setText(screen.getText()+"4");
        }
            
    }else if(e.getSource()== fiveButton){
        
        if (OperatorClicked) {
        screen.setText("5");
        OperatorClicked=false;
        }else{
        screen.setText(screen.getText()+"5");
        }

    }else if (e.getSource()== sixButton){
        
        if (OperatorClicked) {
        screen.setText("6");   
        OperatorClicked=false;
        }else{
        screen.setText(screen.getText()+"6");
        }

    }else if(e.getSource()== oneButton){
        
        if (OperatorClicked) {
        screen.setText("1"); 
        OperatorClicked=false;
        }else{
        screen.setText(screen.getText()+"1");
        }

    }else if(e.getSource()== twoButton){
        
        if (OperatorClicked) {
        screen.setText("2");   
        OperatorClicked=false;    
        }else{
        screen.setText(screen.getText()+"2");
        }

    }else if(e.getSource()== threeButton){
        
        if (OperatorClicked) {
        screen.setText("3");  
        OperatorClicked=false;
        }else{
        screen.setText(screen.getText()+"3");
        }
          
    }else if(e.getSource()== zeroButton){
        
        if (OperatorClicked) {
        screen.setText("0");
        OperatorClicked=false;
        }else{
        screen.setText(screen.getText()+"0");
        }
           
    }else if(e.getSource()== dotButton){
        
        if (!screen.getText().contains(".")) {
        if (OperatorClicked) {
        screen.setText(".");   
        OperatorClicked=false;
        }else{
        screen.setText(screen.getText()+".");
        }
    }

    // Operatorsss /////////////////////////////////////////////////////////
          
    }else if(e.getSource()== percentageButton){

        OperatorClicked=true;
        Operator="%";
        oldvalue=screen.getText();
        screen.setText("%");

    }else if(e.getSource()== divButton){

        OperatorClicked=true;
        Operator="/";
        oldvalue=screen.getText();
        screen.setText("/");

    }else if(e.getSource()== mulButton){

        OperatorClicked=true;
        Operator="x";
        oldvalue=screen.getText();
        screen.setText("x");

    }else if(e.getSource()== minusButton){

        OperatorClicked=true;
        Operator="-";
        oldvalue=screen.getText();
        screen.setText("-");

    }else if(e.getSource()== plusButton){

        OperatorClicked=true;
        Operator="+";
        oldvalue=screen.getText();
        screen.setText("+");

    }else if(e.getSource()== equalButton){

        newvalue=screen.getText();
        oldvalueFloat=Float.parseFloat(oldvalue); // in here u defiend  float variable dont forget
        newvalueFloat=Float.parseFloat(newvalue); // here too
      //  Result=oldvalueFloat+newvalueFloat;
      

    switch (Operator) {
        case "+":
        Result=oldvalueFloat+newvalueFloat;                
        break;
        case "-":
        Result=oldvalueFloat-newvalueFloat;
        break;

        case "x":
        Result=oldvalueFloat*newvalueFloat;
        break;

        case "%":
        Result = (oldvalueFloat / 100) * newvalueFloat;
        break;

        case "/":
        if (newvalueFloat != 0) {
        Result=oldvalueFloat/newvalueFloat;
        }else{
        screen.setText("Error");
        }
        break;

        default:
        Result=0f;
        break;
        }
        screen.setText(String.valueOf(Result));
    }
    
    else if(e.getSource()== clearButton){
        screen.setText("");

    } else if (e.getActionCommand().equals("DL")) {
        String currentValue=screen.getText();
        if(!currentValue.isEmpty()){
        screen.setText(currentValue.substring(0, currentValue.length() - 1));
        }
     
    }

   }
}
