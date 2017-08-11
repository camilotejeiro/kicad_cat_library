KiCad CAT Library Conventions
=============================

_First and Foremost:_
[Regarding KiCad Library Management – No Complaints](https://camilotejeiro.github.io/2016/04/22/regarding-kicad-library-management-no-complaints.html)

_These are largely based on the 
[KiCad Library Conventions](https://github.com/KiCad/kicad-library/wiki/Kicad-Library-Convention) 
with some minor changes based on my experience (completely personal 
choices and these **will** change)._


## Kicad Schematic Sizes
---

_Keep them in Imperial units: KiCad Eeschema only has support for imperial units._

* Pin width (default wire size):        0.006 inches (6 mils)

* Default Drawing width:                0.008 inches (8 mils)  
    But you can use any increment of 0.002 mils if necessary e.g:
    - 0.006 inches.
    - 0.008 inches. Always default to 8 mils to draw symbol outline.
    - 0.01  inches

* Pin length:                           0.1 inches (100 mils)

* Pin number size:                      0.050 inches (50 mils)

* Pin name size:                        0.050 inches (50 mils)

* Pin placement grid:                   0.1 inches  (100mils)

* Text fields (name and value):         0.050 inches (50 mils)  
    Always keep them at 0.050" if they clutter the schematic 
    you can reduce the size in the board schematic directly (not in 
    the original library symbol)

* Text fields clearance:  
    - If edge to edge:                  0.01 inches (10 mils) or, 
    - If center to edge of text field:  0.015 inches (15 mils) 

Also make sure you align the Field text accordingly so that when it expands 
it doesnt overlap with the symbol.


## Kicad Schematic Naming Conventions
---

**Abreviations all caps, otherwise only first letter uppercase.**

_We are not using lower case only, because symbol, land pattern and 3d 
model names follow the convention already, so lets stick to it, 
we'll see._

### Library names (sticking to KLC)

*note that only underscores are used for spaces*

* Generic Library Name example: 
    Use the digikey/mouser product categories as a reference.   
    > Product_Category_Only:          RCL.lib, Bipolar_Transistors_BJT_Single.lib
     
* Manufacturer Library Name Example:  
    > Manufacturer_Specific_Product_Category:  Microchip_PIC16_MCUs.lib

### Symbol Names 

*note that both dashes and underscores are used*

* Generic schematic Symbol Example:  
    > Schematic-Symbol-Description:               C-POL-US, Q-NPN-BCE or BJT-NPN-BCE
    
* Manufacturer schematic Symbol Example: 
    Always append full part number.  
    > Schematic-Symbol-Description_Part-Number:   OPAMP-W-SUPPLY_MCP6001UT-I/OT


## Kicad Land Pattern Creation Steps (Requirements)
---

_For specific SMD Chip IPC compliant resistors, capacitors or inductors 
please refer to your common RCL calculator tool and use those results 
for the individual libraries_

**These are our generic requirements for manufacturer specific parts.**

1. Assembly outline
    - Line width:                               0.15mm

2. Adhesive outline (if applicable)
    - Line width:                               0.01mm
    - Grid increments:                          0.05mm
    - Keep clearance with pad.
    - Adhesive rectangle width less than component width.

3. Component pads.
    - Place the pads as per the component datasheet.
    - No local clearances. You will deal with design rules during layout.

4. Courtyard
    - Line width:                               0.05mm.
    - Courtyard clearance (center to center):   0.25mm

5. Silkscreen Outline (if applicable)
    - line width:                               0.15mm
    - silkscreen clearance:                     0.25mm  
        * To other silkscreen:                  Edge to edge
        * To component pad:                     Edge to Edge.

6. Text Fields
    - height:                                   1mm
    - width:                                    20%
    - Default Clearance (edge to edge):         0.25mm
    - Default Clearance (center to edge):       0.30mm
    - Name field:                               REF**
    - Value field:                              Footprint name.
    - value field is invisible.

7. Footprint properties.
    - Doc Field:        Readable meaningful description of footprint. 
                        This field is very flexible, use linking words and 
                        no abbreviations.                        
    - Keywords:         Footprint name words with no underscores or 
                        dashes (except for manufacturer part name).
    - Populate the footprint properties.
    - Add 3D model if applicable.


## Kicad Land Pattern Naming Conventions
---

**Abreviations all caps, otherwise only first letter uppercase.**

_We are not using lower case only, because symbol, land pattern and 3d 
model names follow the convention already, so lets stick to it, 
we'll see._

### Library names (sticking to KLC)

*note that only underscores are used for spaces*

* Generic Library Name example: 
    Use the name of the standard Land pattern category (Be specific).    
    > Specific_Land_Pattern_Standard:          RCL_SMD_Chip_IPC.lib.
     
* Manufacturer Library Name Example (Be specific):
    > Manufacturer_Specific_Product_Category:  ON_Semiconductor_Linear_Amplifiers.lib

### Land Pattern Names 

*note that both dashes and underscores are used*

* Generic Land Pattern Example:  
    > Land-Pattern-Description:               1608M-0603I-Most
    
* Manufacturer Land Pattern Example:  
    Always use full part number.  
    > Land-Pattern-Description_Part-Number:   SOT-23_BC817-40LT3G


_Always build your libraries on a **need to have basis**, do not build 
parts you don't need (more parts **does not** mean better libraries). 
Otherwise they will go unmaintained and mix with the good parts and 
clutter your libraries making them useless_
