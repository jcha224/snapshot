/**
 * TCSS 305 - SPRING 2016
 * Assignment 4 - SnapShop
 */

package gui;

import filters.EdgeDetectFilter;
import filters.EdgeHighlightFilter;
import filters.Filter;
import filters.FlipHorizontalFilter;
import filters.FlipVerticalFilter;
import filters.GrayscaleFilter;
import filters.SharpenFilter;
import filters.SoftenFilter;

import image.PixelImage;

import java.awt.BorderLayout;
import java.awt.FlowLayout;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import java.io.File;
import java.io.FileWriter;
import java.io.IOException;

import javax.swing.ImageIcon;
import javax.swing.JButton;
import javax.swing.JFileChooser;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JPanel;
import javax.swing.filechooser.FileNameExtensionFilter;





/**
 * This class contains the implementation of the graphical user interface.
 * 
 * @author John Chang
 * @version 28 April 2016
 */
public class SnapShopGUI extends JFrame {
    
    /** Generated serial number UID for object serialization. */
    private static final long serialVersionUID = -869941063501286082L;

    /** The string presented with errors. */
    private static final String ERROR_MESSAGE = "The selected file did not contain an image!";
    
    /** The number of rows in grid layout. */
    private static final int ROW = 7;
    
    /** The file chooser. */
    private final JFileChooser myFileChoose;
    
    /** The status of image in window. */
    private boolean myPicturePresent;
   
    /** The panel that will contain the image. */
    private JPanel myImagePanel;
    
    /** The current file directory. */
    private File myCurrentFile;
    
    /** The image contained in a label. */
    private JLabel myPicLabel;
    
    /** The save button. */
    private JButton mySaveButton = new JButton();
    
    /** The close button. */
    private JButton myCloseButton = new JButton();
    
    /** The edge detect button. */
    private JButton myEdgeDetect; 
    
    /** The edge highlight button. */
    private JButton myEdgeHigh; 
    
    /** The flip horizontal button. */
    private JButton myFlipHor;
    
    /** The flip vertical button. */
    private JButton myFlipVert;
    
    /** The grayscale button. */
    private JButton myGrayscale;
    
    /** The sharpen button. */
    private JButton mySharpen;
    
    /** The soften button. */
    private JButton mySoften;
    
    /** This is the picture. */
    private PixelImage myPicture;

    /**
     * Calls to the super constructor to instantiate a JFrame.
     */
    public SnapShopGUI() {
        super("TCSS 305 SnapShop");
        myFileChoose = new JFileChooser(
                       new File(
                       "C:\\Users\\John\\305\\username-snapshop\\sample_images"));
        final FileNameExtensionFilter filter = new FileNameExtensionFilter(
                                      "Image Files", "jpg", "png", "gif", "jpeg");
        myFileChoose.setFileFilter(filter);
        myPicLabel = new JLabel();
    }

    /**
     * 
     */
    public void start() {
        setLayout(new BorderLayout());
        setLocationRelativeTo(null);
        myImagePanel = new JPanel(new FlowLayout(FlowLayout.LEFT));
        myImagePanel.add(myPicLabel);
        final JPanel buttonsPanel = new JPanel(new BorderLayout());
        buttonsPanel.add(getTopButtons(), BorderLayout.NORTH);
        buttonsPanel.add(getBottomButtons(), BorderLayout.SOUTH);
        
        //javax.swing.JOptionPane.showMessageDialog(null, "SnapShop placeholder");
        add(buttonsPanel, BorderLayout.WEST);
        add(myImagePanel, BorderLayout.CENTER);
        setMinimumSize(getPreferredSize());
        pack();
        setVisible(true);
    }
    
    /**
     * Creates a panel containing the top half of the buttons.
     * @return a panel of buttons
     */
    private JPanel getTopButtons() {
        final JPanel northPanel = new JPanel();
        northPanel.setLayout(new GridLayout(ROW, 1));
        
        myEdgeDetect = new JButton("Edge Detect");
        myEdgeHigh = new JButton("Edge Highlight");
        myFlipHor = new JButton("Flip Horizontal");
        myFlipVert = new JButton("Flip Vertical");
        myGrayscale = new JButton("Grayscale");
        mySharpen = new JButton("Sharpen");
        mySoften = new JButton("Soften");
        
        myEdgeDetect.addActionListener(filterAction(
                                    new EdgeDetectFilter()));
        myEdgeHigh.addActionListener(filterAction(
                                    new EdgeHighlightFilter()));
        myFlipHor.addActionListener(filterAction(
                                    new FlipHorizontalFilter()));
        myFlipVert.addActionListener(filterAction(
                                    new FlipVerticalFilter()));
        myGrayscale.addActionListener(filterAction(
                                    new GrayscaleFilter()));
        mySharpen.addActionListener(filterAction(
                                    new SharpenFilter()));
        mySoften.addActionListener(filterAction(
                                    new SoftenFilter()));
                
        myEdgeDetect.setEnabled(false);
        myEdgeHigh.setEnabled(false);
        myFlipHor.setEnabled(false);
        myFlipVert.setEnabled(false);
        myGrayscale.setEnabled(false);
        mySharpen.setEnabled(false);
        mySoften.setEnabled(false);
        
        northPanel.add(myEdgeDetect);
        northPanel.add(myEdgeHigh);
        northPanel.add(myFlipHor);
        northPanel.add(myFlipVert);
        northPanel.add(myGrayscale);
        northPanel.add(mySharpen);
        northPanel.add(mySoften);
        pack();
        return northPanel;
    }
    
    /**
     * Creates a panel containing the bottom half of the buttons.
     * @return a panel of buttons
     */
    private JPanel getBottomButtons() {
        final JPanel southPanel = new JPanel(new GridLayout(3, 1));
        
        final JButton openButton = new JButton("Open...");
        openButton.addActionListener(openAction());
        
        mySaveButton = new JButton("Save As...");
        mySaveButton.addActionListener(saveAction());
        mySaveButton.setEnabled(false);
        
        myCloseButton = new JButton("Close");
        myCloseButton.addActionListener(new ActionListener() {
            public void actionPerformed(final ActionEvent theEvent) {
                enableButtons(false);
            }
        });
        myCloseButton.setEnabled(false);
        
        southPanel.add(openButton);
        southPanel.add(mySaveButton);
        southPanel.add(myCloseButton);
        pack();
        return southPanel;
    }
    
    /**
     * This opens a folder to retrieve a picture.
     * @return an action listener for open button
     */
    private ActionListener openAction() {
        final ActionListener open = new ActionListener() {
            public void actionPerformed(final ActionEvent theEvent) {
                final int returnVal = myFileChoose.showOpenDialog(SnapShopGUI.this);
                
                if (returnVal == JFileChooser.APPROVE_OPTION) {
                    myCurrentFile = myFileChoose.getSelectedFile();
                    addPicture();
                    pack();
                }
            }
        };
        return open;
    }
    
    /**
     * Sets action to filter buttons.
     * @param theFilter filter used on the button
     * @return action listener to add to button
     */
    private ActionListener filterAction(final Filter theFilter) {
        final ActionListener button = new ActionListener() {
            public void actionPerformed(final ActionEvent theEvent) {
                theFilter.filter(myPicture);
                changePic(myPicture);
                setMinimumSize(getPreferredSize());
            }
        };
        return button;
    }
    
    /**
     * This opens a folder to save a picture.
     * @return an action listener for save button
     */
    private ActionListener saveAction() {
        final ActionListener save = new ActionListener() {
            public void actionPerformed(final ActionEvent theEvent) {
                FileWriter outStream = null;
                
                final int returnVal = myFileChoose.showSaveDialog(SnapShopGUI.this);
                if (returnVal == JFileChooser.APPROVE_OPTION) {
                    myCurrentFile = myFileChoose.getSelectedFile();
                    try {
                        outStream = new FileWriter(myFileChoose.getSelectedFile());
                        outStream.write(myPicLabel.toString());
                    } catch (final IOException e) {
                        e.printStackTrace();
                    }
                }
                
            } };
        return save;
    }
    
    /**
     * This enables and disables buttons and can remove the image.
     * @param theVar boolean value to enable or disable
     */
    private void enableButtons(final boolean theVar) {
        mySaveButton.setEnabled(theVar);
        myCloseButton.setEnabled(theVar);
        myEdgeDetect.setEnabled(theVar);
        myEdgeHigh.setEnabled(theVar);
        myFlipHor.setEnabled(theVar);
        myFlipVert.setEnabled(theVar);
        myGrayscale.setEnabled(theVar);
        mySharpen.setEnabled(theVar);
        mySoften.setEnabled(theVar);
        myImagePanel.setVisible(theVar);
        if (!theVar) {
            myPicturePresent = theVar;
            myImagePanel.remove(myPicLabel);
            myPicLabel = new JLabel();
            myImagePanel.add(myPicLabel);
            setMinimumSize(getPreferredSize());
            pack();
        }
        
    }
    
    /**
     * This is a helper method for open action listener.
     */
    private void addPicture() {
        boolean validImage = true;
        if (myPicturePresent) {
            myImagePanel.remove(myPicLabel);
            myPicLabel = new JLabel();
        }
        try {
            myPicture = PixelImage.load(myCurrentFile);
            if (myPicture == null) {
                javax.swing.JOptionPane.showMessageDialog(null, ERROR_MESSAGE);
                validImage = false;
                enableButtons(false);
            }
        } catch (final IOException ex) {
            javax.swing.JOptionPane.showMessageDialog(null, ERROR_MESSAGE);
            validImage = false;
            enableButtons(false);
        }
        if (validImage) {
            myPicLabel.setIcon(new ImageIcon(myPicture));
            myImagePanel.add(myPicLabel);
            myPicturePresent = true;
            enableButtons(true);
            setMinimumSize(getPreferredSize());
        }
    }
    
    /** 
     * Adds filter to the image.
     * @param theImage is the new version of the image
     */
    private void changePic(final PixelImage theImage) {
        myImagePanel.remove(myPicLabel);
        myImagePanel.revalidate();
        myPicLabel = new JLabel();
        myPicLabel.setIcon(new ImageIcon(theImage));
        myImagePanel.add(myPicLabel);
        setMinimumSize(getPreferredSize());
    }

}