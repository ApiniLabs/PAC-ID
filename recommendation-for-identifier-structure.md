
# How to Structure the Identifier of a ``PAC-ID``

While the basic specification for the `PAC-ID` has been intentionally kept minimal, `PAC-ID`s are much more powerful if they are issued both, systematically and with a bit of verbosity. This page contains recommendations how to structure the `identifier` of the `PAC-ID`. 
They are designed around these goals goals:

- Verbose enough so that it is always clear
  - to what the ID is pointing to
  - what the uniqueness scope is
- Reliable and easy for service discovery with PAC-ID Resolver

## Recommended Structure of the `identifier`
It is RECOMMENDED to use this structure of the `identifier`:
![Segment groups](images/identifier_structure.png)


The following chapters explain the composition in more detail.


## Identify the Category
`PAC-ID`s might be used to identify various different categories of entities. Entities of different categories are treated differently (e.g. a substance can be aliquoted, while a device cannot; a method instructs a device what to do, while a run documents what was done). <br>
In order to account for these differences the first identifier segment MUST [^1] indicate the category.

![Segment groups](images/identifier_structure_category-id.png)


These categories MUST [^1] by used:
**category_key** |**Main** |**Sub**| **Meaning** |
| :--- | :--- | :--- | :--- |
|`MD` | M | D | **Device** <br> _uniquely identifiable item, non-aliquotable, not dividable_| 
 `MS` | M | S | **Substance** <br> Source Material, Aliquot, Sample, Product <br> _uniquely identifiable item, aliquotable/dividable_ |
| `MC` | M | C | **Consumable** <br> (typically bulk goods with limited lifespan) <br> _uniquely identifiable type of item, typically countable_ 
|`MM` | M | M | **Misc Material** <br> _anything that doesn’t fit other M types - **ideally never used**_ 
| `DC` | D | C | **Calibration** <br> Basic Configuration | changeable but valid for all DM/DP/DR 
| `DM` | D | M | **Method** <br> Run Configuration, Receipe, SOP | a definition of a certain process 
| `DP` | D | P | **Progress** <br> Status Update, Live Data <br> _data of time-limited validity occurring while a DM is executed._
| `DR` | D | R | **Result** <br> Completed Run Data, Report, CoA <br> _data that is a direct result of a completed DM run._
| `DS` | D | S | **Static Properties** <br> metadata, datasheet, master data, physical properties. <br> _Unchangeable, universally true_ 





## Segment Structure Within a Category 
It is RECOMMENDED to use the following segment structure within a category:

![Segment groups](images/identifier_structure_category-segments.png)

Example of a balance:
```
HTTPS://PAC.METTORIUS.COM/-MD/240:BAL500/21:210263/8008:20230205/8009:ABC
                              |recommended segments|custom segments       |
                           ^ category key
```

### Recommened Segments per Category
Within a category the segments SHOULD follow this structure:
|[Category](#categories) | Segments|
|:---|:---|
**Materials**
Device | **`-MD` <br>`240` (Model number) <br> `21`  (Serial number)** <br>
Substance | **`-MS` <br> `240`  (Product number)** <br> `10`  (Batch number) <br> `20`  (Container size) <br> `21`  (Container number) <br> `250` (Aliquot)
Consumable |**`-MC` <br> `240`  (Product number)** <br> `10` (Batch number) <br> `20` (Packaging size) <br> `21` (Serial number) <br> `250`  (Aliquot)
Misc | **`-MM` <br> `240` (Product number)** <br> `10`  (Batch Number) <br> `20` (Packaging size) <br> `21` (Serial number) <br> `250` (Aliquot)


Segments in bold MUST [^1] be used, the other segments SHOULD be added if they are available. The order SHOULD be preserved, even of optional segments are omitted.


### Custom Segments:
If nessecary custom segements CAN be added. If so, they MUST be placed after the recommended segments.

### Short Notation
In oder to reduce the number of characters a short form MAY be used. 

```
HTTPS://PAC.METTORIUS.COM/-MD/BAL500/210263/8008:20230205
```

The short notation omits the keys for segments of each category. Keys are implicitly assigned based on the [segment order](#Best-practice-for-segment-structure-within-a-category) until an explicit key that differs is reached or an ID segment starting with “-“ is reached.
Explicit keys can be used along implicit ones, as long as the order of segments is matched.

e.g. for ``HTTPS://PAC.METTORIUS.COM/-MD/240:BAL500/210263/8008:20230205``, 210263 is still regarded to have implicit key 21. For ``HTTPS://PAC.METTORIUS.COM/-MD/240:BAL500/8008:20230205/210263`` we can’t auto-assign a key for 12345432 as it is preceded by a segment with an explicit key. 12345432 is therefore interpreted as a custom segment.



## Category Concatenation
Imagine a `PAC-ID` that points to a result set of a device. We’d usually want to know on which device that result was created. We CAN simply concatenate categories (in this case a material category to a data category):

![Segment groups](images/identifier_structure_category-concatenation.png)

Example:
```
HTTPS://PAC.METTORIUS.COM/-DR/240:123ABC/8008:20230205/-MD/240:BAL500/21:210263
                         | primary category           | additional category
```

The advantage of this is that it allows resolving device related attributes and services (e.g. device operation manual,…) via the same coupling table information entries also used for `PAC-ID`s relating to a device.

The category of the item the `PAC-ID` is referring to, SHALL [^1] be the first category.. 


[^1]: Altough is not mandatory to follow the recommenation on this page, this rule MUST be applied **if** the identifier is structured according to the recommendations on this page.