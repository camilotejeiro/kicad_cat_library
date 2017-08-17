KiCad CAT Library Rules
=======================

_First and Foremost:_
[Regarding KiCad Library Management – No Complaints](https://camilotejeiro.github.io/2016/04/22/regarding-kicad-library-management-no-complaints.html).

_This document was largely based on [KiCad Library Conventions](https://github.com/KiCad/kicad-library/wiki/Kicad-Library-Convention)._ 

However, there are some minor differences for compliance with industry standards 
(e.g. IEEE, IPC ...etc) and based on my design experience (completely personal 
choices and these **will** change).

## Use of this document
---

When building library components:

1. Follow the rules in this document first: these take prevalence over KLC.

If you need additional guidelines (**and there are no rule conflicts**): 

2. Follow the KLC reference in every section.

## 0. Library Structure
---

Component libraries are always categorized in generic-functional (for common 
low-pin count) and manufacturer-based parts, this makes component-reuse 
possible. 

* note that every generic directory (3d_packages, schematic_symbols and 
    land_patterns) must have a standards.txt file indicating the official 
    standard used when building each generic part in the library.

Here is a short example:

~~~
kicad_library
├── generic_3d_packages
│   ├── Capacitors_SMD_Chip_IPC.3dshapes
│   │   ├── 1608M-0603I.wrl
│   │   ...
│   ├── Pin_Headers_Imperial.3dshapes
│   │   ├── 01X02-0.1IN-Straight-TH.wrl
│   │   ...
|   ├── Resistors_SMD_Chip_IPC.3dshapes
│   │   ├── 1608M-0603I.wrl
│   │   ... 
│   └── standards.txt
├── generic_land_patterns
│   ├── Capacitors_SMD_Chip_IPC.pretty
│   │   ├── 1608M-0603I-Nominal.kicad_mod
│   │   ...
│   ├── Pin_Headers_Imperial.pretty
│   │   ├── 01X02-0.1IN-Straight-TH.kicad_mod
│   │   ...
│   ├── Resistors_SMD_Chip_IPC.pretty
│   |   ├── 1608M-0603I-Nominal.kicad_mod
|   |   ...
│   └── standards.txt   
├── generic_schematic_symbols
│   ├── Bipolar_Transistors_BJT_Single.bck
│   ├── Bipolar_Transistors_BJT_Single.dcm
│   ├── Bipolar_Transistors_BJT_Single.lib
│   ├── Connectors.bck
│   ├── Connectors.dcm
│   ├── Connectors.lib
│   ├── RCL.bck
│   ├── RCL.dcm
│   ├── RCL.lib
|   |   ...
│   └── standards.txt   
├── manufacturer_3d_packages
│   └── ON_Semiconductor_Bipolar_Transistors.3dshapes
│       ├── SOT-23_BC817-40LT3G.wrl
│       ...
├── manufacturer_land_patterns
│   └── ON_Semiconductor_Bipolar_Transistors.pretty
│       ├── SOT-23_BC817-40LT3G.kicad_mod
│       ... 
├── manufacturer_schematic_symbols
...
~~~

## 1. General Rules
---

_[KLC1 Reference](https://github.com/KiCad/kicad-library/wiki/Kicad-Library-Convention#1-general-rules)._ 

**Remember: Abbreviations all caps, otherwise only first letter uppercase.**

* **Always build your personal library on a need to have basis**  
    Do not build parts you don't need (more parts **does not** mean better 
    libraries). _Otherwise they will go unmaintained and mix with the 
    good parts and clutter your libraries making them useless_

* **Only include in your project the library files you absolutely need in your design**   
    You don't need hundreds of libraries included in your project when you are
    only using 2 or 3 at most, this is a great way to make mistakes. 
    **Keep your project workspace clean.** 

* Pin names and numbers (for generic-functional parts i.e. common low-pin-count components)  
    + Pin numbers: should follow lower-case letter conventions if pin functions 
        are available (e.g. bec for BJTs, gsd for MOSFETs ...etc), 
        otherwise use standard numbers (e.g. 123...etc for connectors).   
    + Pin names: should describe pin functions if available (e.g. Base,
        Emitter, Collector for BJTs ...etc), otherwise use same numbers as pin
        number.    

* Pin names and numbers (for manufacturer parts)  
    + Pin numbers: Generally for high-pin-count parts, pin numbers should match 
        numbers used in the datasheet, except for some common manufacturer parts 
        (e.g. BJTs, MOSFETs, Diodes ...etc) where you should use lower-case
        letter convention (to allow for generic schematic-pcb part association)
    + Pin names: should describe pin functions if available, otherwise use same
        numbers as pin number.

## 2. Symbol Library names (Naming Conventions)
---

_[KLC2 Reference](https://github.com/KiCad/kicad-library/wiki/Kicad-Library-Convention#2-symbol-library-names-lib-files)._ 

**Note: only underscores are used for spaces**

* Generic Library Name example 
    Use the digikey/mouser product categories as a reference.   
    > Product_Category_Only:                    RCL.lib, Bipolar_Transistors_BJT_Single.lib
     
* Manufacturer Library Name Example  
    > Manufacturer_Specific_Product_Category:   Microchip_PIC16_MCUs.lib

## 3. Symbol Names (Naming Conventions)
---

_[KLC3 Reference](https://github.com/KiCad/kicad-library/wiki/Kicad-Library-Convention#3-symbol-names)._ 

**Note: both dashes and underscores are used.** We are not using underscore 
only (see 2016 textpad notes). Also symbol, land pattern and 
3d model names follow the convention already: this is supported by KLC.

* Symbol name shall not repeat words/naming from the library name.

* Generic schematic Symbol Example  
    > Schematic-Symbol-Description:               C-POL-US, Q-NPN-BCE or BJT-NPN-BCE
    
* Manufacturer schematic Symbol Example  
    Always append full part number.  
    > Schematic-Symbol-Description_Part-Number:   OPAMP-W-SUPPLY_MCP6001UT-I/OT

## 4. General Rules for Symbols (Drawing Conventions) 
---

_[KLC4 Reference](https://github.com/KiCad/kicad-library/wiki/Kicad-Library-Convention#4-general-rules-for-symbols)._

**Keep them in Imperial units:** This is what is used in standards(IEC-60617), 
plus KiCad Eeschema only has support for imperial units.

**Default grid:** 50 mils.

* (1) Pin placement
    + Pin spacing/grid
        - Recommended: 100 mil grid with 100 mil spacing between pins.  
        - Minimum: 50 mil grid with 50 mil spacing between pins.
    + Pin length
        - Recommended (L=100n): Length from 0 to 300 mils at integer multiples
          of 100 (e.g. 0, 100, 200, 300).
          - 0 mils length: _Useful for pins with invisible pin names and numbers,_ 
          common for small low-pin-count discrete components 
            (e.g. resistors, capacitors, inductors, FETs, BJTs ...etc)
          - 100 mils length or more: _Useful for pins with visible descriptive
            pin names and numbers_, common for high-pin-count and/or IC
            components (e.g. MCUs, SOCs, OPAMPs, ADCs ...etc)
            components, 
        - Min (L=50n): Length from 0 to 300 mils at integer multiples of 50
          (e.g. 0, 50, 100 ... 300). Useful for complex symbols or
          high-pin-count components.

* (2) Symbol visual style
    + Symbol origin
        - Recommended: Center of symbol strongly recommended 
            (but not required). For complex symbols other constraints take
            precedence.
    + Symbol body line with
        - Required: 10 mils  
    + Symbol standard type
        - Recommended: IEEE 315-1975 or other EE standard. 

* Symbol drawing grid 
    + Recommended: Start from the default grid and go down to smaller grids for 
        drawing the symbol finer details.
    + Minimum: 5 mils is the smallest grid you can use to draw symbol details. 
    
* (8) Text fields size
    + Required: 50 mils for all  

    Always keep them at 50 mils if they clutter the schematic 
    you can reduce the size in the schematic directly (not in 
    the original library symbol)

* Text fields placement 
    + Required: Use 25 mil grid and make sure: 
        - If edge to edge min 10 mils of clearance or,  
        - If center to edge of text field min 15 mils of clearance.  
    
    Also make sure you align the Field text accordingly so that when it expands 
    it doesn't overlap with the symbol.

* (9) Default Symbol Fields
    + Value: The name of the symbol 
        - Required: Follow symbol naming conventions. 
            - In schematic, gets replaced by the component value with units.
            - For voltage sources it will be replaced with +5V, +1.8V ...etc, 
                for gnd it will be invisible by default, but can be set 
                visible and set to AGND, DGND ...etc.
    + Reference Designator
        - For discrete components: Use designator names from EE standards.
        - For power and graphical symbols: Use #PWR and #SYM respectively.

    Also, do not define a component properties as "power symbol" this locks the
    value field and limits component re-use.
    
* (10) Part meta-data.
    + Description field: describe the component, free-form (no rules)
    + Keywords field: Choose the keywords (space separated) that will help you 
        find the components easily from the library chooser.

* (13) Power Symbols (V+, GND ...etc) 
    + Required: Contain pin set to Power Output (for ERC check)

## 5. Footprint Library Naming Conventions (Land Pattern Naming Conventions)
---

_[KLC5 Reference](https://github.com/KiCad/kicad-library/wiki/Kicad-Library-Convention#5-footprint-library-naming-conventions)._ 

**Note: only underscores are used for spaces.**

* Generic Library Name example 
    Use the name of the standard Land pattern category (Be specific)    
    > Specific_Land_Pattern_Standard:          RCL_SMD_Chip_IPC.lib.
     
* Manufacturer Library Name Example (Be specific)
    > Manufacturer_Specific_Product_Category:  ON_Semiconductor_Linear_Amplifiers.lib

## 6. Footprint Naming Conventions (Land Pattern Naming Conventions) 
---

_[KLC6 Reference](https://github.com/KiCad/kicad-library/wiki/Kicad-Library-Convention#6-footprint-naming-conventions)._ 

**Note: both dashes and underscores are used.** We are not using underscore 
only (see 2016 textpad notes). Also symbol, land pattern and 
3d model names follow the convention already: this is supported by KLC.

* Footprint name shall not repeat words/naming from the library name.

* Generic Land Pattern Example  
    > Land-Pattern-Description:               1608M-0603I-Most
    
* Manufacturer Land Pattern Example  
    Always use full part number.  
    > Land-Pattern-Description_Part-Number:   SOT-23_BC817-40LT3G

## 7. General Rules for Footprints 
---

_[KLC7 Reference](https://github.com/KiCad/kicad-library/wiki/Kicad-Library-Convention#7-general-rules-for-footprints)._ 

**For specific SMD Chip IPC compliant resistors, capacitors or inductors:** 
please refer to your common RCL calculator tool and use those results 
for the individual libraries.

* (3) Silkscreen Layer (IPC-7351C)
    + (i) Reference Designator (F.silkS layer)  
        - (a) Text Size
            - 1.0mm  
        - (b) Text thickness 
            - 0.15mm (15%) recommended 
            - aternatively 20% (thicker)  
        - (c) Fully visible placement
    + (ii) Silkscreen Clearance
        - (a) No placement over pads
        - (b) Min clearance from pads             
            - 0.2mm
        - Default Clearance(edge to edge)
            - 0.25mm
        - Default Clearance (center to edge)
            - 0.30mm
    + (iii) Visible after board assembly (for SMD components)
    + (iv) Visible after board assembly (for TH components)
    + (v) Silkscreen line width   
        - Low density (default)
            - 0.15mm  
        - Mid density
            - 0.12mm    
        - High density
            - 0.10mm  
    + (vi) Pin-1 designator marker required  
    + (vii) Pin-1 designator must always be visible (after fab and assembly)  
    + (viii) Pin-1 designator as per IPC-7351C  

* (4) Fabrication Layer 
    + (i) Component value (footprint name) should be provided on F.Fab layer
        - (a) Text size                       
            - 1.00mm
        - (b) Text thickness                      
            - 0.15mm
    + (ii) Component outline should be provided on the appropriate F.Fab layer
        - (a) Line width                          
            - Low density (default): 0.15mm
            - High density:          0.10mm  
        - (b) Outline should be simplified for complex shapes
        - (c) Pin-1 designation is provided on F.Fab layer where appropriate
    + (iii) Reference Designator should also be provided on F.Fab layer
        - (a) Centered on component (inside component outline)
        - (b) Size of text matched to component size (should fit inside component 
            outline)
        - (c) Recommended text size               
            - 1.00mm
        - (d) Allowable text size                
            - 0.1mm to 2.00mm
        - (e) Allowable text thickness            
            - 0.01mm to 0.20mm (recommended 15% of text size, with allowances 
                for variations)

* (5) Courtyard Layer  
    + (i) Courtyard Layer                         
        - F.CrtYd layer   
    + (ii) Courtyard line width                       
        - 0.05mm line width  
    + (iii) Courtyard placement grid                  
        - 0.01mm  
    + (iv) Clearance is measured from exterior of pads and package outline  
        - (a) Default courtyard clearance             
            - 0.25mm  
        - (b) Components smaller than 0603            
            - 0.15mm  
        - (c) Connectors, canned capacitors, crystals 
            - 0.5mm  
        - (d) BGA footprints                           
            - 1.0mm  
            
* Adhesive outline (if applicable)
    + Line width
        - 0.05mm
    + Grid increments
        - 0.01mm
    + Keep clearance with pad
    + Adhesive rectangle width less than component width

## 8. Rules for Surface Mount Devices (SMD) Footprints (Land Patterns) 
---

_[KLC8 Reference](https://github.com/KiCad/kicad-library/wiki/Kicad-Library-Convention#8-rules-for-surface-mount-devices-smd-footprints)._ 

* (2) Footprint anchor should be placed in the middle of the footprint (IPC-7351) 
    Generally this is the centroid calculated with respect to the device lead ends
    + (i) If the datasheet specifies an origin for Pick-and-Place, this should 
        be used in preference

* (3) Pad layer settings
    + (i) Front copper 
        - F.Cu  
    + (ii) Front Mask
        - F.Mask  
    + (iii) Front paste 
        - F.Paste
 
* Place the pads as per the component datasheet  

* No local clearances. You will deal with design rules during layout 

## 9. Rules for Through Hole Technology (THT) Footprints (Land Patterns)
---
_[KLC9 Reference](https://github.com/KiCad/kicad-library/wiki/Kicad-Library-Convention#9-rules-for-through-hole-technology-tht-footprints)._ 

* (2) Modified: **Footprint anchor should be set on center.** Otherwise, 
    layout rotation gets messy (read annoying)   

* (5) Minimum drilled hole diameter is the maximum lead diameter plus 0.20mm 
    (IPC-2222 Class 2)

* (6) Minimum annular ring width should be at least 0.15mm (IPC-2221)

## 10. Footprint properties
---
_[KLC10 Reference](https://github.com/KiCad/kicad-library/wiki/Kicad-Library-Convention#10-footprint-properties)._ 

* (1) Footprint name must match its filename (.kicad_mod files)  

* (2) Footprint (properties) meta-data should be filled in as appropriate   
    + (i) Documentation field contains comma-separated device information 
        Where appropriate URL to footprint datasheet should be included
    + Readable meaningful description of footprint  
        This field is very flexible, use linking words and no abbreviations., 
    + (ii) Keywords field contains space-separated keyword values   
    + Footprint name words with no underscores or dashes (except for 
        manufacturer part name)

* (4) 3D Shape files should be named the same as their footprint and are placed in 
    a folder named the same as the footprint library replacing the .pretty with 
    .3dshapes  
    + (iv) 3D model references should be added even if the model does not yet exist 
        (this helps with library maintenance)

