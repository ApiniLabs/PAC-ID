
TODO: Explain that this structure is recommended (not must): However the intention is that IF the structure is used the parts of it are "mandatory".
How to explain this best

# How to structure the identifier 
The specification of a pac ID was intentionally kept short. However it is highly RECOMMENDED to structure the `identifier` of the PAC-ID like so:
![Segment groups](images/identifier_structure.png)


The following chapters explain the composition in more detail:

## Identify the category
PAC-IDs might be used to identify various different categories of entities. Entities of different categories are treated differently (e.g. a substance can be aliquoted, while a device cannot; a method instructs a device what to do, while a run documents what was done). <br>
In order to account for these differences the first identifier segment SHOULD indicate the category.

![Segment groups](images/identifier_structure_category-id.png)


These categories SHOULD by used:
| **Meaning** | **Characteristics**| **category_segment** |
| :--- | :--- | :--- |
| **Materials**||||
| **Device** | uniquely identifiable item, non-aliquotable, not dividable| `-MD` |
| **Substance** <br> Source Material, Aliquot, Sample, Product | uniquely identifiable item, aliquotable/dividable | `-MS` |
| **Consumable** <br> (typically bulk goods with limited lifespan) | uniquely identifiable type of item, typically countable | `-MC` |
| **Misc Material** | anything that doesn’t fit other M types - ideally never used |`-MM` |
**Data**
| **Calibration** <br> Basic Configuration | changeable but valid for all DM/DP/DR | `-DC` |
| **Method** <br> Run Configuration, Receipe, SOP | a definition of a certain process | `-DM` |
| **Progress** <br> Status Update, Live Data | data of time-limited validity occurring while a DM is executed. | `-DP` |
| **Result** <br> Completed Run Data, Report, CoA | data that is a direct result of a completed DM run. | `-DR` | 
| **Static properties** |  metadata, datasheet, master data, physical properties. Unchangeable, universally true | `-DS` |



## Segment structure within a category 
It is RECOMMENDED to use the following segment structure within a category:

![Segment groups](images/identifier_structure_category-segments.png)

Example of a balance:
```
HTTPS://PAC.METTORIUS.COM/-MD/240:BAL500/21:1234567/8008:20230205/8009:ABC
                              |recommended segments|custom segments       |
                           ^ category key
```



<!-- |[Category](#categories) | | | | | | |
|:---|:---|:---|:---|:---|:---|:---|
Device | `-MD` | `240` <br> (Model number) * | `21` <br> (Serial number) *|
Substance | `-MS` | `240` <br> (Product number) * | `10` <br> (Batch number) | `20` <br> (Container size) | `21` <br> (Container number) | `250` <br> (Aliquot)
Consumable | `-MC` | `240` <br> (Product number) * | `10` <br> (Batch number) | `20` <br> (Packaging size) | `21` <br> (Serial number) | `250` <br> (Aliquot)
Misc | `-MM` | `240` <br> (Product number) * | `10` <br> (Batch Number) | `20` <br> (Packaging size) | `21` <br> (Serial number) | `250` <br> (Aliquot) -->

### Recommened segments per category
Within a category the segments SHOULD follow this structure:
|[Category](#categories) | Segments|
|:---|:---|
**Materials**
Device | `-MD` <br>`240`  (Model number) * <br> `21`  (Serial number) *<br>
Substance | `-MS` <br> `240`  (Product number) * <br> `10`  (Batch number) <br> `20`  (Container size) <br> `21`  (Container number) <br> `250` (Aliquot)
Consumable | `-MC` <br> `240`  (Product number) * <br> `10` (Batch number) <br> `20` (Packaging size) <br> `21` (Serial number) <br> `250`  (Aliquot)
Misc | `-MM` <br> `240` (Product number) * <br> `10`  (Batch Number) <br> `20` (Packaging size) <br> `21` (Serial number) <br> `250` (Aliquot)
**Data**
TODO: Structure for DX segments

Segments with an * SHOULD be used, the other segments CAN be added if they are available. The order SHOULD be preserved, even of optional segments are omitted.


### Custom segments:
If nessecary custom segements CAN be added. If they are, they SHOULD be placed after the recommended segments.

### Short notation
In oder to reduce the number of characters a short form MAY be used. 

```
HTTPS://PAC.METTORIUS.COM/-MD/BAL500/12345432/8008:20230205
```

The short notation omits the keys for segments of each category. Keys are implicitly assigned based on the [segment order](#Best-practice-for-segment-structure-within-a-category) until an explicit key that differs is reached or an ID segment starting with “-“ is reached.
Explicit keys can be used along implicit ones, as long as the order of segments is matched.





e.g. for ``HTTPS://PAC.METTORIUS.COM/-MD/240:R300/12345432/8008:20230205``, 12345432 is still regarded to have implicit key 21. For ``HTTPS://PAC.METTORIUS.COM/-MD/240:R300/8008:20230205/12345432`` we can’t auto-assign a key for 12345432 as it is preceded by a segment with an explicit key. 12345432 is therefore interpreted as a custom ID segment.



## Category concatenation
Imagine a PAC-ID that points to a result set of a device. We’d usually want to know on which device that result was created. We CAN simply concatenate  categories (in this case a material category to a data category):

![Segment groups](images/identifier_structure_category-concatenation.png)

Example:
```
HTTPS://PAC.METTORIUS.COM/-DR/240:123ABC/8008:20230205/-MD/240:BAL2/21:123456
                         | primary category           | additional category
```

The advantage of this is that it allows resolving device related attributes and services (e.g. device operation manual,…) via the same coupling table information entries also used for PAC-ID’s relating to a device.

It is RECOMMENDED that the category of the item the PAC-ID is referring to, is the first category.. 


