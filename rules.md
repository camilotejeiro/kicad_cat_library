KiCad CAT Library Rules
=======================

_First and Foremost:_
[Regarding KiCad Library Management – No Complaints](https://camilotejeiro.github.io/2016/04/22/regarding-kicad-library-management-no-complaints.html).

_This document is largely based on [KiCad Library Conventions](https://github.com/KiCad/kicad-library/wiki/Kicad-Library-Convention)._ 

However, there are some minor differences for compliance with industry standards 
(e.g. IEEE, IPC ...etc) and based on my design experience (completely personal 
choices and these **will** change).

## Use of this document
---

When building library components:

1. Follow the rules in this document first: these take prevalence over KLC.

If you need additional guidelines: 

2. Follow the KLC reference in every section, **but only if there are no rule 
    conflicts (with my library rules)**.

## 0. Library Structure
---

Component libraries are always categorized in generic-functional (for common 
low-pin count) and manufacturer-based parts, this makes component-reuse 
possible. Here is a short example:

~~~
kicad_library
├── generic_3d_packages
│   ├── Capacitors_SMD_Chip_IPC.3dshapes
│   │   ├── 1608M-0603I.wrl
│   │   ...
│   ├── Pin_Headers_Imperial.3dshapes
│   │   ├── 01X02-0.1IN-Straight-TH.wrl
│   │   ...
│   └── Resistors_SMD_Chip_IPC.3dshapes
│       ├── 1608M-0603I.wrl
│       ... 
├── generic_land_patterns
│   ├── Capacitors_SMD_Chip_IPC.pretty
│   │   ├── 1608M-0603I-Nominal.kicad_mod
│   │   ...
│   ├── Pin_Headers_Imperial.pretty
│   │   ├── 01X02-0.1IN-Straight-TH.kicad_mod
│   │   ...
│   └── Resistors_SMD_Chip_IPC.pretty
│       ├── 1608M-0603I-Nominal.kicad_mod
│       ...
├── generic_schematic_symbols
│   ├── Bipolar_Transistors_BJT_Single.bck
│   ├── Bipolar_Transistors_BJT_Single.dcm
│   ├── Bipolar_Transistors_BJT_Single.lib
│   ├── Connectors.bck
│   ├── Connectors.dcm
│   ├── Connectors.lib
│   ├── RCL.bck
│   ├── RCL.dcm
│   └── RCL.lib
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

* (1) Pin placement (additional rules added to be able to draw components accurately) 
    + (i)  Pin spacing
        - Spacing at more than 100mils or integer multiples of 100mil (IEC-60617) 
    + Pin placement
        - Recommended to fall on 100 mils grid (from center), otherwise.
        - At min must fall on the 50 mils grid (from center).
    + (ii) Pin length (min)
        - More than 100 mils  
    + (iii) Pin length (max)
        - Less than 300 mils  
    + (iv) Pin length increments
        - 50 mils

* (2) Symbol visual style
    + (i) Symbol origin
        - Center of symbol recommended (but not required).  
            Other constraints (e.g. pin placement have precedence)
    + (ii) Symbol body line with
        - 10 mils  
    + (iii) Symbol body background
        - Fill background     
    + (iv) Symbol standard type
        - IEEE 315-1975  

* Default drawing width: **10 mils**  
    But you can use any increment of +/-2 mils if really necessary e.g:  
    + 12 mil
    + 10 mil: default 
    + 8 mil 
    + 6 mil

* Default drawing grid: **50 mils** (default for Eeschema)  
    But you can use smaller grids as necessary e.g: 
    + 25 mil
    + 10 mil ... etc.  
    When drawing resistors, capacitors, transistors ...etc, 
    you need finer details.  
    
    _However, make sure to preserve all other pin placement and symbol guidelines._

* (8) Text fields size: 50 mils for all  
    + (i) Value field  
    + (ii) Reference field  
    + (iii) Footprint field  
    + (iv) Datasheet field  
    + (v) Pin names and numbers field  

    Always keep them at 50 mils if they clutter the schematic 
    you can reduce the size in the schematic directly (not in 
    the original library symbol)

* Text fields placement 
    + Use 25 mil grid and make sure: 
        - If edge to edge: min 10 mils or,  
        - If center to edge of text field: min 15 mils   
    
    Also make sure you align the Field text accordingly so that when it expands 
    it doesn't overlap with the symbol.

* (10) Part meta-data.
    + (i) Description field: describe the component, free-form (no rules)
    + (iv) Keywords: Choose the keywords (space separated) that will 
        help you find the components from the library chooser.

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

