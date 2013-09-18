First Steps
===========

## First steps

The simplest way to load a PDB file is by using the [StructureIO](http://www.biojava.org/docs/api/org/biojava3/structure/StructureIO.html) class.

<pre>
     public static void main(String[] args){

        try {
                Structure structure = StructureIO.getStructure("4HHB");
                // and let's print out how many atoms are in this structure
                System.out.println(StructureTools.getNrAtoms(structure));
            } catch (Exception e){
                e.printStackTrace();
        }
    }   
</pre>

BioJava  automatically downloads the PDB file for hemoglobin [4HHB](http://www.rcsb.org/pdb/explore.do?structureId=4HHB) and copies it into a temporary location. Then the PDB file parser loads the data into a [Structure](http://www.biojava.org/docs/api/org/biojava/bio/structure/Structure.html) object, that provides access to the content in the file. (If you call this a second time, BioJava will automatically re-use the local file.)

<table>
    <tr>
        <td>
            <a href="http://www.rcsb.org/pdb/explore.do?structureId=4hhb"><img src="img/4hhb_bio_r_250.jpg"/></a>
        </td>
        <td>
            The crystal structure of human deoxyhaemoglobin PDB ID <a href="http://www.rcsb.org/pdb/explore.do?structureId=4hhb">4HHB</a> (image source: <a href="http://www.rcsb.org/pdb/explore.do?structureId=4hhb">RCSB</a>)
    </tr>
</table>



This demonstrates two things:

+ BioJava can automatically download and install files locally (more on this in Chapter 4)
+ BioJava by default writes those files into a temporary location (The system temp directory "java.io.tempdir"). 

If you already have a local PDB installation, you can configure where BioJava should read the files from by setting the PDB_DIR system property

<pre>
    -DPDB_DIR=/wherever/you/want/
</pre>

## A Quick 3D View

If you have the *biojava-structure-gui* module installed, you can quickly visualise a [Structure](http://www.biojava.org/docs/api/org/biojava/bio/structure/Structure.html) via this:

<pre>
    public static void main(String[] args){
    
        try {
            
            Structure struc = StructureIO.getStructure("4hhb");

            StructureAlignmentJmol jmolPanel = new StructureAlignmentJmol();

            jmolPanel.setStructure(struc);

            // send some commands to Jmol
            jmolPanel.evalString("select * ; color chain;");            
            jmolPanel.evalString("select *; spacefill off; wireframe off; cartoon on;  ");
            jmolPanel.evalString("select ligands; cartoon off; wireframe 0.3; spacefill 0.5; color cpk;");
            
        } catch (Exception e){
            e.printStackTrace();
        }
    }
</pre>

This will result in the following view:

<table>
    <tr>
        <td>
            <img src="img/4hhb_jmol.png"/>
        </td>
        <td>
            The <a href="http://www.biojava.org/docs/api/org/biojava/bio/structure/align/gui/jmol/StructureAlignmentJmol.html">StructureAlignmentJmol</a> class provides a wrapper for the <a href="http://jmol.sourceforge.net/">Jmol</a> viewer and provides a bridge to BioJava, so Structure objects can be sent to Jmol for visualisation.
        </td>
    </tr>
</table>   