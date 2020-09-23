<div align="center">

## JCalendar


</div>

### Description

A generic java class to select date graphically, similar to the date picker in windows.
 
### More Info
 
Date (String) in the following formats -

DD-MM-YY

DD-MM-YYYY

DD-MON-YY

DD-MON-YYYY

Please mail me if any....


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Praveen Kumar G](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/praveen-kumar-g.md)
**Level**          |Intermediate
**User Rating**    |5.0 (20 globes from 4 users)
**Compatibility**  |Java \(JDK 1\.2\), Java \(JDK 1\.3\), Java \(JDK 1\.4\), Java \(JDK 1\.5\)
**Category**       |[Controls/ Forms/ Graphics/ Menus](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/controls-forms-graphics-menus__2-59.md)
**World**          |[Java](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/java.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/praveen-kumar-g-jcalendar__2-4602/archive/master.zip)





### Source Code

/*
 * JCalendar.java
 *
 * Created on December 11, 2004, 6:52 PM
 */
package com.cal;
import java.util.*;
/**
 * <B>JCalendar</B> is a class for graphically
 * picking a date.
 * @author Praveen Kumar G
 * @email pikz{@}mail.com
 * © Praveen Kumar G, Dec 2004
 */
public class JCalendar extends javax.swing.JPanel implements java.awt.event.MouseListener{
 // Fields Declaration
 /**
  * Field specifying date to be returned in <B>DD-MM-YY</B> format.<br>
  * eg: 02-04-1999
  */
 public static final int DD_MM_YY = 0;
 /**
  * Field specifying date to be returned in <B>DD-MM-YYYY</B> format.<br>
  * eg: 02-04-1999
  */
 public static final int DD_MM_YYYY = 1;
 /**
  * Field specifying date to be returned in <B>DD-MON-YY</B> format.<BR>
  * eg: 02-JAN-99
  */
 public static final int DD_MON_YY = 2;
 /**
  * Field specifying date to be returned in <B>DD-MON-YYYY</B> format.<BR>
  * eg: 02-JAN-1999
  */
 public static final int DD_MON_YYYY = 3;
 /**
  * Creates new JCalendar object.
  */
 public JCalendar() {
  initComponents();
  clearDays();
  setYears();
  Calendar rightNow = Calendar.getInstance();
  month = rightNow.get(Calendar.MONTH);
  day = rightNow.get(Calendar.DATE);
  year = rightNow.get(Calendar.YEAR);
  selDay = day;
  selMonth = month;
  selYear = year;
  setDate(rightNow);
  addListeners();
  for ( int j =0; j < daysPanel.getComponentCount(); j++){
   javax.swing.JLabel tLabel = (javax.swing.JLabel) daysPanel.getComponent(j);
   tLabel.setBorder(new javax.swing.border.EmptyBorder(1,1,1,1));
  }
 }
 private void clearDays(){
  for ( int j =0; j < daysPanel.getComponentCount(); j++){
   javax.swing.JLabel tLabel = (javax.swing.JLabel) daysPanel.getComponent(j);
   tLabel.setText(" ");
   tLabel.setForeground(new java.awt.Color(0,0,0));
  }
 }
 private void setYears(){
  yearCombo.removeAllItems();
  for(int i = 1990; i <= 2009; i++)
   yearCombo.addItem(new String("" + i));
 }
 private void setDate(Calendar nowCal){
  month = nowCal.get(Calendar.MONTH);
  day = nowCal.get(Calendar.DATE);
  year = nowCal.get(Calendar.YEAR);
  monthCombo.setSelectedIndex(month);
  yearCombo.setSelectedItem(Integer.toString(year));
  clearDays();
  renderDays();
 }
 private void renderDays(){
  // method to render the days on the grid
  // Get the first day of the week
  for ( int j =0; j < daysPanel.getComponentCount(); j++){
   javax.swing.JLabel tLabel = (javax.swing.JLabel) daysPanel.getComponent(j);
   tLabel.setBorder(new javax.swing.border.EmptyBorder(1,1,1,1));
  }
	Calendar presCal = Calendar.getInstance();
  int pYear = presCal.get(Calendar.YEAR);
  int pMonth = presCal.get(Calendar.MONTH);
  int pDay = presCal.get(Calendar.DATE);
  Calendar dateCal = Calendar.getInstance();
  dateCal.set(year, month, 1);
  dateCal.set(Calendar.DAY_OF_MONTH,1);
  firstday = dateCal.get(Calendar.DAY_OF_WEEK);
  javax.swing.JLabel jl = (javax.swing.JLabel) daysPanel.getComponent(firstday-1);
  noofdays = dateCal.getActualMaximum(Calendar.DAY_OF_MONTH);
  //jl.setText("" + 1);
  for(int k = 0; k < noofdays; k++){
   jl = (javax.swing.JLabel) daysPanel.getComponent(firstday+k-1);
    jl.setForeground(new java.awt.Color(0,0,0));
   jl.setText(Integer.toString(k+1));
   jl.setForeground((k+1==pDay && month==pMonth && year==pYear) ? (new java.awt.Color(66,132,213)) : java.awt.Color.BLACK);
  }
 }
 private void addListeners(){
  for ( int j =0; j < daysPanel.getComponentCount(); j++){
   javax.swing.JLabel tLabel = (javax.swing.JLabel) daysPanel.getComponent(j);
   tLabel.addMouseListener(this);
  }
 }
 /**
  * Method returning the selected date.
  * @return Returns the selected date in the format specified by the format.
  * @see See the fields for more information.
  * @param format One of the four fields specifying the return format of the date.
  */
 public String getDate(int format){
  String rDate = "";
  switch(format){
   case DD_MM_YY:
    rDate = selDay + "-" + selMonth + "-" + new String("" + selYear).substring(2);
    break;
   case DD_MM_YYYY:
    rDate = selDay + "-" + selMonth + "-" + selYear;
    break;
   case DD_MON_YY:
    rDate = selDay + "-" + monthVals[selMonth] + "-" + new String("" + selYear).substring(2);
    break;
   case DD_MON_YYYY:
    rDate = selDay + "-" + monthVals[selMonth] + "-" + selYear;
    break;
   default:
    rDate = selDay + "-" + selMonth + "-" + new String("" + selYear).substring(2);
    break;
  }
  return rDate;
 }
 public void mouseClicked(java.awt.event.MouseEvent mouseEvent) {
				Calendar presCal = Calendar.getInstance();
  int pYear = presCal.get(Calendar.YEAR);
  int pMonth = presCal.get(Calendar.MONTH);
  int pDay = presCal.get(Calendar.DATE);
  int tDay;
  javax.swing.JLabel jl = (javax.swing.JLabel) mouseEvent.getComponent();
  jl.setForeground(new java.awt.Color(66,132,213));
  if(jl.getText() != " "){
   for ( int j =0; j < daysPanel.getComponentCount(); j++){
    javax.swing.JLabel tLabel = (javax.swing.JLabel) daysPanel.getComponent(j);
    tLabel.setBorder(new javax.swing.border.EmptyBorder(1,1,1,1));
    tDay=0;
    if(tLabel.getText() != " "){
     tDay = Integer.parseInt(tLabel.getText());
    }
    tLabel.setForeground((tDay==pDay && month==pMonth && year==pYear) ? (new java.awt.Color(66,132,213)) : java.awt.Color.BLACK);
   }
   jl.setBorder(new javax.swing.border.LineBorder(new java.awt.Color(0,128,64)));
   jl.setForeground(new java.awt.Color(66,132,213));
   selDay = Integer.parseInt(jl.getText());
   selMonth = month;
   selYear = year;
  }
 }
 /** This method is called from within the constructor to
  * initialize the form.
  */
 private void initComponents() {
  monthCombo = new javax.swing.JComboBox();
  yearCombo = new javax.swing.JComboBox();
  basePanel = new javax.swing.JPanel();
  weekDaysPanel = new javax.swing.JPanel();
  jLabel1 = new javax.swing.JLabel();
  jLabel2 = new javax.swing.JLabel();
  jLabel3 = new javax.swing.JLabel();
  jLabel4 = new javax.swing.JLabel();
  jLabel5 = new javax.swing.JLabel();
  jLabel6 = new javax.swing.JLabel();
  jLabel7 = new javax.swing.JLabel();
  daysPanel = new javax.swing.JPanel();
  setLayout(null);
  monthCombo.setModel(new javax.swing.DefaultComboBoxModel(new String[] { "January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December" }));
  monthCombo.addActionListener(new java.awt.event.ActionListener() {
   public void actionPerformed(java.awt.event.ActionEvent evt) {
    monthComboActionPerformed(evt);
   }
  });
  add(monthCombo);
  monthCombo.setBounds(10, 10, 100, 22);
  yearCombo.addActionListener(new java.awt.event.ActionListener() {
   public void actionPerformed(java.awt.event.ActionEvent evt) {
    yearComboActionPerformed(evt);
   }
  });
  add(yearCombo);
  yearCombo.setBounds(120, 10, 110, 22);
  basePanel.setLayout(new java.awt.BorderLayout());
  basePanel.setBorder(new javax.swing.border.EtchedBorder());
  weekDaysPanel.setLayout(new java.awt.GridLayout(1, 7));
  weekDaysPanel.setBackground(new java.awt.Color(204, 204, 255));
  jLabel1.setBackground(new java.awt.Color(255, 255, 255));
  jLabel1.setHorizontalAlignment(javax.swing.SwingConstants.CENTER);
  jLabel1.setText("Su");
  weekDaysPanel.add(jLabel1);
  jLabel2.setBackground(new java.awt.Color(255, 255, 255));
  jLabel2.setHorizontalAlignment(javax.swing.SwingConstants.CENTER);
  jLabel2.setText("Mo");
  weekDaysPanel.add(jLabel2);
  jLabel3.setBackground(new java.awt.Color(255, 255, 255));
  jLabel3.setHorizontalAlignment(javax.swing.SwingConstants.CENTER);
  jLabel3.setText("Tu");
  weekDaysPanel.add(jLabel3);
  jLabel4.setBackground(new java.awt.Color(255, 255, 255));
  jLabel4.setHorizontalAlignment(javax.swing.SwingConstants.CENTER);
  jLabel4.setText("We");
  weekDaysPanel.add(jLabel4);
  jLabel5.setBackground(new java.awt.Color(255, 255, 255));
  jLabel5.setHorizontalAlignment(javax.swing.SwingConstants.CENTER);
  jLabel5.setText("Th");
  weekDaysPanel.add(jLabel5);
  jLabel6.setBackground(new java.awt.Color(255, 255, 255));
  jLabel6.setHorizontalAlignment(javax.swing.SwingConstants.CENTER);
  jLabel6.setText("Fr");
  weekDaysPanel.add(jLabel6);
  jLabel7.setBackground(new java.awt.Color(255, 255, 255));
  jLabel7.setHorizontalAlignment(javax.swing.SwingConstants.CENTER);
  jLabel7.setText("Sa");
  weekDaysPanel.add(jLabel7);
  basePanel.add(weekDaysPanel, java.awt.BorderLayout.NORTH);
  daysPanel.setLayout(new java.awt.GridLayout(6, 0));
  daysPanel.setBackground(new java.awt.Color(255, 255, 255));
  daysLabel = new javax.swing.JLabel[42];
  for(int i = 0; i < 42; i++){
  	daysLabel[i] = new javax.swing.JLabel();
			daysLabel[i].setHorizontalAlignment(javax.swing.SwingConstants.CENTER);
  	daysLabel[i].setText("...");
  	daysPanel.add(daysLabel[i]);
		}
  basePanel.add(daysPanel, java.awt.BorderLayout.CENTER);
  add(basePanel);
  basePanel.setBounds(10, 40, 220, 180);
 }
 private void yearComboActionPerformed(java.awt.event.ActionEvent evt) {
  year = Integer.parseInt(yearCombo.getSelectedItem().toString());
  java.util.Calendar cal = java.util.Calendar.getInstance();
  cal.set(year,month,day);
  setDate(cal);
 }
 private void monthComboActionPerformed(java.awt.event.ActionEvent evt) {
  month = monthCombo.getSelectedIndex();
  java.util.Calendar cal = java.util.Calendar.getInstance();
  cal.set(year,month,day);
  setDate(cal);
 }
 public void mouseEntered(java.awt.event.MouseEvent mouseEvent) {
 }
 public void mouseExited(java.awt.event.MouseEvent mouseEvent) {
 }
 public void mousePressed(java.awt.event.MouseEvent mouseEvent) {
 }
 public void mouseReleased(java.awt.event.MouseEvent mouseEvent) {
 }
 // Variables declaration
 private javax.swing.JPanel basePanel;
 private javax.swing.JPanel daysPanel;
 private javax.swing.JLabel jLabel1;
 private javax.swing.JLabel jLabel2;
 private javax.swing.JLabel jLabel3;
 private javax.swing.JLabel jLabel4;
 private javax.swing.JLabel jLabel5;
 private javax.swing.JLabel jLabel6;
 private javax.swing.JLabel jLabel7;
 private javax.swing.JComboBox monthCombo;
 private javax.swing.JPanel weekDaysPanel;
 private javax.swing.JComboBox yearCombo;
 private javax.swing.JLabel[] daysLabel;
 int month;
 int day;
 int year;
 int firstday = 0;
 int noofdays = 0;
 int selDay = 0;
 int selMonth = 0;
 int selYear = 0;
 private String[] monthVals = {"JAN","FEB","MAR","APR","MAY","JUN","JUL","AUG","SEP","OCT","NOV","DEC"};
}

