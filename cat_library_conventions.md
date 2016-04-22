Camilo Library Conventions
==========================

*First and Foremost:*
[Regarding KiCad Library Management – No Complaints](https://camilotejeiro.wordpress.com/2016/04/21/regarding-kicad-library-management-no-complaints/)

These are largely based on the KiCad Library Conventions with some minor 
changes based on my experience (completely personal choices).

## Kicad Land Pattern Creation Steps (Requirements)

These are our generic requirements for manufacturer parts.

*For specific SMD Chip IPC compliant numbers please refer to your 
calculator tool and use those results*

1. Assembly outline
    - line width:                               0.15mm

2. Adhesive outline (if applicable)
    - line width:                               0.01mm
    - Grid increments:                          0.05mm
    - Keep clearance with pad.
    - Adhesive rectangle width Less than component width.

3. Component pads.
    Place the component pads.
    No local clearances. You will deal with design rules during layout.

4. Courtyard
    - line width:                               0.05mm.
    - courtyard clearance (center to center):   0.25mm

5. Silkscreen Outline (if applicable)
    - line width:                               0.15mm
    - silkscreen clearance:                     0.25mm

6. Text Fields
    - Default Clearance:                        0.25mm
    - height:                                   1mm
    - width:                                    20%
    - Name field:                               REF**
    - Value field:                              Footprint name.
    - value field is invisible.

8. Footprint properties.
    - Populate the footprint properties.
    - Add 3D model.


## Kicad Schematic Sizes

Keep them in Imperial units: KiCad only has support for imperial units.

* Pin width (default wire size):        0.006 inches (6 mils)

* Default Drawing width:                0.008 inches (8 mils)
    But you can use any increment of 0.002 mils if necessary.
    e.g.
    0.006 inches.
    0.008 inches. Always default to 8 mils to draw symbol outline.
    0.01  inches

* Pin length:                           0.1 inches (100 mils)

* Pin number size:                      0.050 inches (50 mils)

* Pin name size:                        0.050 inches (50 mils)

* Pin placement grid:                   0.1 inches  (100mils)

* Text fields (name and value):         0.050 inches (50 mils)
    Always keep them at 0.050" if they clutter the schematic 
    you can reduce the size in the board schematic directly (not in 
    the original library symbol)
    
* text fields clearance (edge to edge): 0.01 inches (10 mils)
    15 mils center to edge of text field.

Also make sure you align the Field text accordingly so that when it expands 
it doesnt overlap with the symbol.


## Kicad Land Pattern Naming Conventions


### Library names (sticking to KLC)

Abreviations all caps, otherwise only first letter uppercase. 

We are not using lower case only, because symbol, land pattern and 3d 
model names follow the convention already, so lets stick to it, 
we'll see. 

Generic Library Name example: 
Use the name of the standard Land pattern category (Be specific).
    Specific_Land_Pattern_Standard:          RCL_SMD_Chip_IPC.lib.
     
Manufacturer Library Name Example 
    Manufacturer_Specific_Product_Category:  On_Semiconductor_Linear_Amplifiers.lib

### Land Pattern Names 

abreviations all caps, otherwise only first letter uppercase. Always 
use full part number.

Generic Land Pattern Example
    Land-Pattern-Description:               RCL-1608M-0603I-Most
    
Manufacturer Land Pattern Example 
    Land-Pattern-Description_Part-Number:   SOT-23_BC817-40LT3G

## Kicad Schematic Naming Conventions

### Library names (sticking to KLC)

Abreviations all caps, otherwise only first letter uppercase. 

We are not using lower case onl, because symbol, land pattern and 3d 
model names follow the convention already, so lets stick to it, 
we'll see. 

Generic Library Name example: 
Use the digikey/mouser product categories as a reference. 
    Product_Category_Only:          RCL.lib, Bipolar_Transistors_BJT_Single.lib
     
Manufacturer Library Name Example 
    Manufacturer_Product_Category:  On_Semiconductor_Linear_Amplifiers.lib

### Symbol Names 

abreviations all caps, otherwise only first letter uppercase. Always 
use full part number.

Generic schematic Symbol Example
    Schematic-Symbol-Description:               C-POL-US, Q-NPN-BCE
    
Manufacturer schematic Symbol Example 
    Schematic-Symbol-Description_Part-Number:   OPAMP-W-SUPPLY_MCP6001UT-I/OT
