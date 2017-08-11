KiCad CAT Library Conventions
=============================

_First and Foremost:_
[Regarding KiCad Library Management – No Complaints](https://camilotejeiro.github.io/2016/04/22/regarding-kicad-library-management-no-complaints.html)

_We will try to keep this document up to date and stick with 
[KiCad Library Conventions.](https://github.com/KiCad/kicad-library/wiki/Kicad-Library-Convention)_ 
Especially when official IEEE standards are followed (assume KLC unless otherwise noted). 

However, there will be some minor differences based on my experience (completely personal 
choices and these **will** change).

## 1. General Rules
---

_same as KLC,_ plus a couple of other important tips.

**Remember: Abbreviations all caps, otherwise only first letter uppercase.**

* **Always build your libraries on a need to have basis.**  
    Do not build parts you don't need (more parts **does not** mean better 
    libraries). _Otherwise they will go unmaintained and mix with the 
    good parts and clutter your libraries making them useless_

* **Only include in your project the library files you absolutely need in your design.**   
    You don't need hundreds of libraries included in your project when you are
    only using 2 or 3 at most, this is a great way to make mistakes. 
    **Keep your project workspace clean.** 

## 2. Symbol Library names (Naming Conventions)
---

_Same as KLC_

**Note: only underscores are used for spaces**

* Generic Library Name example: 
    Use the digikey/mouser product categories as a reference.   
    > Product_Category_Only:                    RCL.lib, Bipolar_Transistors_BJT_Single.lib
     
* Manufacturer Library Name Example:  
    > Manufacturer_Specific_Product_Category:   Microchip_PIC16_MCUs.lib

## 3. Symbol Names (Naming Conventions)
---

_Additional to KLC_

**Note: both dashes and underscores are used.** We are not using lower 
case only, because symbol, land pattern and 3d model names follow the convention 
already: this is supported by KLC.

* Generic schematic Symbol Example:  
    > Schematic-Symbol-Description:               C-POL-US, Q-NPN-BCE or BJT-NPN-BCE
    
* Manufacturer schematic Symbol Example: 
    Always append full part number.  
    > Schematic-Symbol-Description_Part-Number:   OPAMP-W-SUPPLY_MCP6001UT-I/OT

## 4. General Rules for Symbols (Drawing Conventions) 
---

_Same as KLC._ Some important sections re-written for clarity.

**Keep them in Imperial units:** This is what is used in standards(IEC-60617), 
plus KiCad Eeschema only has support for imperial units.

1. Pin placement (re-written for clarity)  

    i.   Pin placement grid:        100mils (IEC-60617)  
    ii.  Pin length (min):          > 100 mils  
    iii. Pin length (max):          < 300 mils  
    iii. Pin length increments:     50 mils   

2. Symbol visual style (re-written for clarity)  

    i.   Symbol origin:             Middle of symbol  
    ii.  Symbol body line with:     10 mils  
    iii. Symbol body background:    Fill background     
    iv.  Symbol standard type:      IEEE 315-1975  

* Default Drawing width:            10 mils  
    But you can use any increment of +/-2 mils if really necessary e.g:  
    
    - 6 mil.
    - 8 mil 
    - 10 mil: default 

8. Text fields size: 50 mils for all  

    i.   Value field  
    ii.  Reference field  
    iii. Footprint field  
    iv.  Datasheet field  
    v.   Pin names and numbers field.  

    Always keep them at 50 mils if they clutter the schematic 
    you can reduce the size in the schematic directly (not in 
    the original library symbol)

* Text fields clearance:   
 
    - If edge to edge:                  0.01 inches (10 mils) or,  
    - If center to edge of text field:  0.015 inches (15 mils)   

Also make sure you align the Field text accordingly so that when it expands 
it doesn't overlap with the symbol.

## 5. Footprint Library Naming Conventions (Land Pattern Naming Conventions)
---

_same as KLC_

**Note: only underscores are used for spaces.**

* Generic Library Name example: 
    Use the name of the standard Land pattern category (Be specific).    
    > Specific_Land_Pattern_Standard:          RCL_SMD_Chip_IPC.lib.
     
* Manufacturer Library Name Example (Be specific):
    > Manufacturer_Specific_Product_Category:  ON_Semiconductor_Linear_Amplifiers.lib

## 6. Footprint Naming Conventions (Land Pattern Naming Conventions) 
---

_Additional to KLC_

**Note: both dashes and underscores are used.** We are not using lower 
case only, because symbol, land pattern and 3d model names follow the 
convention already: this is supported by KLC.

* Generic Land Pattern Example:  
    > Land-Pattern-Description:               1608M-0603I-Most
    
* Manufacturer Land Pattern Example:  
    Always use full part number.  
    > Land-Pattern-Description_Part-Number:   SOT-23_BC817-40LT3G

## 7. General Rules for Footprints 
---

_Same as KLC,_ some important sections re-written for clarity.

**For specific SMD Chip IPC compliant resistors, capacitors or inductors:** 
please refer to your common RCL calculator tool and use those results 
for the individual libraries.

3. Silkscreen Layer (IPC-7351C)

    i. Reference Designator (F.silkS layer).  
        
        a. Text Size:                           1.0mm  
        b. Text thickness:                      0.15mm (15%), aternatively 20% (thicker)  
        c. Fully visible placement.

    ii. Silkscreen Clearance
  
        a. No placement over pads.
        b. Min clearance from pads:             0.2mm 
        * Default Clearance(edge to edge)       0.25mm
        * Default Clearance (center to edge):   0.30mm

    iii. Visible after board assembly (for SMD components).
    iv. Visible after board assembly (for TH components).

    v. Silkscreen line width   

        - Low density (default):                0.15mm  
        - Mid density                           0.12mm    
        - High density                          0.10mm  
    
    vi. Pin-1 designator marker required.  
    vii. Pin-1 designator must always be visible (after fab and assembly).  
    viii. Pin-1 designator as per IPC-7351C.  

4. Fabrication Layer 

    i. Component value (footprint name) should be provided on F.Fab layer

        a. Text size:                           1.00mm
        b. Text thickness:                      0.15mm

    ii. Component outline should be provided on the appropriate F.Fab layer

        a. Line width                          
            - Low density (default):            0.15mm
            - High density:                     0.10mm  
        b. Outline should be simplified for complex shapes
        c. Pin-1 designation is provided on F.Fab layer where appropriate

    iii. Reference Designator should also be provided on F.Fab layer

        a. Centered on component (inside component outline)
        b. Size of text matched to component size (should fit inside component outline)
        c. Recommended text size:               1.00mm
        d. Allowable text size:                 0.1mm to 2.00mm
        e. Allowable text thickness:            0.01mm to 0.20mm 
            approximately 15% of text size, with allowances for variation.

5. Courtyard Layer  

    i. Courtyard Layer:                             F.CrtYd layer   
    ii. Courtyard line width:                       0.05mm line width  
    iii. Courtyard placement grid:                  0.01mm  
    iv. Clearance is measured from exterior of pads and package outline  
        a. Default courtyard clearance:             0.25mm  
        b. Components smaller than 0603:            0.15mm  
        c. Connectors, canned capacitors, crystals: 0.5mm  
        d. BGA footprints                           1.0mm  

## 8. Rules for Surface Mount Devices (SMD) Footprints (Land Patterns) 
---

2. Footprint anchor should be placed in the middle of the footprint (IPC-7351). 
    Generally this is the centroid calculated with respect to the device lead ends.
    
    i. If the datasheet specifies an origin for Pick-and-Place, this should be used in preference.

3. Pad layer settings:

    i. Front copper (F.Cu)  
    ii. Front Mask (F.Mask)  
    iii. Front paste (F.Paste) 
 
* Place the pads as per the component datasheet.  
* No local clearances. You will deal with design rules during layout. 

## 9. Rules for Through Hole Technology (THT) Footprints (Land Patterns)
---
**Different from KLC**

2.. **Footprint anchor should be set on center**    

5.. Minimum drilled hole diameter is the maximum lead diameter plus 0.20mm (IPC-2222 Class 2)

6.. Minimum annular ring width should be at least 0.15mm (IPC-2221)

## 10. Footprint properties
---

1. Footprint name must match its filename. (.kicad_mod files)  

2. Footprint (properties) meta-data should be filled in as appropriate
    
    i. Documentation field contains comma-separated device information. 
        Where appropriate URL to footprint datasheet should be included
    
    * Readable meaningful description of footprint.  
        This field is very flexible, use linking words and no abbreviations., 
    
    ii. Keywords field contains space-separated keyword values
    
    * Footprint name words with no underscores or dashes (except for 
        manufacturer part name).

3. 3D Shape files should be named the same as their footprint and are placed in 
    a folder named the same as the footprint library replacing the .pretty with 
    .3dshapes  

    iii. 3D model references should be added even if the model does not yet exist 
        (this helps with library maintenance)

**These are our generic requirements for manufacturer specific parts.**

## 10. Additional Land Pattern Properties
---

* Adhesive outline (if applicable)

    - Line width:                               0.05mm
    - Grid increments:                          0.01mm
    - Keep clearance with pad.
    - Adhesive rectangle width less than component width.

