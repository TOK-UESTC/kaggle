# PROJECT DOC

# 选题: 房价预测
```
* 开题时间: 2021-06-20
* 负责人: Psy-UESTC
* 人员: Stepen、rocinate、Psy-UESTC
* 结题时间: 2021-07-04
```
# 学习方式
* 基本模型(手刻基本模型, 最初版)
* 调用ML工具包找出较优解
* 学习较优模型(源码解读)



# 任务规划

## week-1 基本模型构建
* task-1 
```
了解特征的现实意义
```
* task-2
```
缺省值填充
```
* task-3
```
非数值类型数据编码
```
* task-4
```
异常值清洗
```

* task-5
```
了解预处理方法、可视化数据
```

* task-6
```
筛选特征值
```

* task-7
```
归一标准化、建立基本模型(线性回归)
```

## week-2 优化模型

* task-1
```
查阅资料尝试不同模型
```

* task-2
```
查看kernel、复现kernel
```

* task-end
```
总结模型算法、形成文档
```



# 任务进度

## task-1  了解特征的现实意义

> time： 2021-06-21
>
> member:  Stepen
>
>  



>MSSubClass: Identifies the type of dwelling involved in the sale.	
>
>        20	1-STORY 1946 & NEWER ALL STYLES
>        30	1-STORY 1945 & OLDER
>        40	1-STORY W/FINISHED ATTIC ALL AGES
>        45	1-1/2 STORY - UNFINISHED ALL AGES
>        50	1-1/2 STORY FINISHED ALL AGES
>        60	2-STORY 1946 & NEWER
>        70	2-STORY 1945 & OLDER
>        75	2-1/2 STORY ALL AGES
>        80	SPLIT OR MULTI-LEVEL
>        85	SPLIT FOYER
>        90	DUPLEX - ALL STYLES AND AGES
>       120	1-STORY PUD (Planned Unit Development) - 1946 & NEWER
>       150	1-1/2 STORY PUD - ALL AGES
>       160	2-STORY PUD - 1946 & NEWER
>       180	PUD - MULTILEVEL - INCL SPLIT LEV/FOYER
>       190	2 FAMILY CONVERSION - ALL STYLES AND AGES
>
>MSZoning(房屋区域): Identifies the general zoning classification of the sale.
>       A	Agriculture
>       C	Commercial
>       FV	Floating Village Residential
>       I	Industrial
>       RH	Residential High Density
>       RL	Residential Low Density
>       RP	Residential Low Density Park 
>       RM	Residential Medium Density
>
>LotFrontage: Linear feet of street connected to property(房屋周围的道路宽度)
>
>LotArea: Lot size in square feet(住房面积)
>
>Street: Type of road access to property(道路类型)
>
>       Grvl	Gravel(石子路)	
>       Pave	Paved(水泥路)
>
>Alley: Type of alley access to property(进入房屋的小巷类型)
>
>       Grvl	Gravel
>       Pave	Paved
>       NA 	No alley access(没有小巷)
>
>LotShape: General shape of property(房屋形状)
>
>       Reg	Regular	(规则)
>       IR1	Slightly irregular(稍微不规则)
>       IR2	Moderately Irregular(中等不规则)
>       IR3	Irregular(不规则)
>
>LandContour: Flatness of the property(房屋平整度)
>
>       大概描述房屋周围的自然环境
>       Lvl	Near Flat/Level
>       Bnk	Banked - Quick and significant rise from street grade to building
>       HLS	Hillside - Significant slope from side to side
>       Low	Depression(萧条)
>
>Utilities: Type of utilities available(设施(水电气等))
>       AllPub	All public Utilities (E,G,W,& S)	
>       NoSewr	Electricity, Gas, and Water (Septic Tank)
>       NoSeWa	Electricity and Gas Only
>       ELO	Electricity only	
>
>LotConfig: Lot configuration
>
>       Inside	Inside lot
>       Corner	Corner lot(转角地段)
>       CulDSac	Cul-de-sac(死巷)
>       FR2	Frontage on 2 sides of property(两面环节)
>       FR3	Frontage on 3 sides of property
>
>LandSlope: Slope of property(倾斜程度)
>		
>       Gtl	Gentle slope
>       Mod	Moderate Slope	
>       Sev	Severe Slope
>
>Neighborhood: Physical locations within Ames city limits(物理位置)
>
>       Blmngtn	Bloomington Heights(Bloomington山庄)
>       Blueste	Bluestem
>       BrDale	Briardale
>       BrkSide	Brookside
>       ClearCr	Clear Creek
>       CollgCr	College Creek
>       Crawfor	Crawford
>       Edwards	Edwards
>       Gilbert	Gilbert
>       IDOTRR	Iowa DOT and Rail Road
>       MeadowV	Meadow Village
>       Mitchel	Mitchell
>       Names	North Ames
>       NoRidge	Northridge
>       NPkVill	Northpark Villa
>       NridgHt	Northridge Heights
>       NWAmes	Northwest Ames
>       OldTown	Old Town
>       SWISU	South & West of Iowa State University
>       Sawyer	Sawyer
>       SawyerW	Sawyer West
>       Somerst	Somerset
>       StoneBr	Stone Brook
>       Timber	Timberland
>       Veenker	Veenker
>
>Condition1: Proximity to various conditions(附近的条件)
>	
>       Artery	Adjacent to arterial street
>       Feedr	Adjacent to feeder street	
>       Norm	Normal	
>       RRNn	Within 200' of North-South Railroad
>       RRAn	Adjacent to North-South Railroad
>       PosN	Near positive off-site feature--park, greenbelt, etc.
>       PosA	Adjacent to postive off-site feature
>       RRNe	Within 200' of East-West Railroad
>       RRAe	Adjacent to East-West Railroad
>
>Condition2: Proximity to various conditions (if more than one is present)
>		
>       Artery	Adjacent to arterial street
>       Feedr	Adjacent to feeder street	
>       Norm	Normal	
>       RRNn	Within 200' of North-South Railroad
>       RRAn	Adjacent to North-South Railroad
>       PosN	Near positive off-site feature--park, greenbelt, etc.
>       PosA	Adjacent to postive off-site feature
>       RRNe	Within 200' of East-West Railroad
>       RRAe	Adjacent to East-West Railroad
>
>BldgType: Type of dwelling(住房类型)
>		
>       1Fam	Single-family Detached	
>       2FmCon	Two-family Conversion; originally built as one-family dwelling
>       Duplx	Duplex
>       TwnhsE	Townhouse End Unit
>       TwnhsI	Townhouse Inside Unit
>
>HouseStyle: Style of dwelling(住房风格)
>	
>       1Story	One story
>       1.5Fin	One and one-half story: 2nd level finished
>       1.5Unf	One and one-half story: 2nd level unfinished
>       2Story	Two story
>       2.5Fin	Two and one-half story: 2nd level finished
>       2.5Unf	Two and one-half story: 2nd level unfinished
>       SFoyer	Split Foyer
>       SLvl	Split Level
>
>OverallQual: Rates the overall material and finish of the house(评估房屋的整体材料和装修)
>
>       10	Very Excellent
>       9	Excellent
>       8	Very Good
>       7	Good
>       6	Above Average
>       5	Average
>       4	Below Average
>       3	Fair
>       2	Poor
>       1	Very Poor
>
>OverallCond: Rates the overall condition of the house(评估这所房子的整体状况)
>
>       10	Very Excellent
>       9	Excellent
>       8	Very Good
>       7	Good
>       6	Above Average	
>       5	Average
>       4	Below Average	
>       3	Fair
>       2	Poor
>       1	Very Poor
>
>YearBuilt: Original construction date（建成年份）
>
>YearRemodAdd: Remodel date(改建日期) (same as construction date if no remodeling or additions)
>
>RoofStyle: Type of roof(屋顶情况)
>
>       Flat	Flat
>       Gable	Gable
>       Gambrel	Gabrel (Barn)
>       Hip	Hip
>       Mansard	Mansard
>       Shed	Shed
>
>RoofMatl: Roof material(屋顶材料)
>
>       ClyTile	Clay or Tile
>       CompShg	Standard (Composite) Shingle
>       Membran	Membrane
>       Metal	Metal
>       Roll	Roll
>       Tar&Grv	Gravel & Tar
>       WdShake	Wood Shakes
>       WdShngl	Wood Shingles
>
>Exterior1st: Exterior covering on house(房屋外墙覆盖物)
>
>       AsbShng	Asbestos Shingles
>       AsphShn	Asphalt Shingles
>       BrkComm	Brick Common
>       BrkFace	Brick Face
>       CBlock	Cinder Block
>       CemntBd	Cement Board
>       HdBoard	Hard Board
>       ImStucc	Imitation Stucco
>       MetalSd	Metal Siding
>       Other	Other
>       Plywood	Plywood
>       PreCast	PreCast	
>       Stone	Stone
>       Stucco	Stucco
>       VinylSd	Vinyl Siding
>       Wd Sdng	Wood Siding
>       WdShing	Wood Shingles
>
>Exterior2nd: Exterior covering on house (if more than one material)
>
>       AsbShng	Asbestos Shingles
>       AsphShn	Asphalt Shingles
>       BrkComm	Brick Common
>       BrkFace	Brick Face
>       CBlock	Cinder Block
>       CemntBd	Cement Board
>       HdBoard	Hard Board
>       ImStucc	Imitation Stucco
>       MetalSd	Metal Siding
>       Other	Other
>       Plywood	Plywood
>       PreCast	PreCast
>       Stone	Stone
>       Stucco	Stucco
>       VinylSd	Vinyl Siding
>       Wd Sdng	Wood Siding
>       WdShing	Wood Shingles
>
>MasVnrType: Masonry veneer type(表层砌体类型)
>
>       BrkCmn	Brick Common
>       BrkFace	Brick Face
>       CBlock	Cinder Block
>       None	None
>       Stone	Stone
>
>MasVnrArea: Masonry veneer area in square feet(砌体贴面面积(平方英尺))
>
>ExterQual: Evaluates the quality of the material on the exterior (在外观上评估材料的质量)
>		
>       Ex	Excellent
>       Gd	Good
>       TA	Average/Typical
>       Fa	Fair
>       Po	Poor
>
>ExterCond: Evaluates the present condition of the material on the exterior(评估外部材料的现状)
>		
>       Ex	Excellent
>       Gd	Good
>       TA	Average/Typical
>       Fa	Fair
>       Po	Poor
>
>Foundation: Type of foundation(地面类型)
>		
>       BrkTil	Brick & Tile
>       CBlock	Cinder Block
>       PConc	Poured Contrete	
>       Slab	Slab
>       Stone	Stone
>       Wood	Wood
>
>BsmtQual: Evaluates the height of the basement（评估地下室的高度）
>
>       Ex	Excellent (100+ inches)	
>       Gd	Good (90-99 inches)
>       TA	Typical (80-89 inches)
>       Fa	Fair (70-79 inches)
>       Po	Poor (<70 inches
>       NA	No Basement
>
>BsmtCond: Evaluates the general condition of the basement(评估地下室的一般情况)
>
>       Ex	Excellent
>       Gd	Good
>       TA	Typical - slight dampness allowed
>       Fa	Fair - dampness or some cracking or settling
>       Po	Poor - Severe cracking, settling, or wetness
>       NA	No Basement
>
>BsmtExposure: Refers to walkout or garden level walls(采光行(不太确定))
>
>       Gd	Good Exposure
>       Av	Average Exposure (split levels or foyers typically score average or above)	
>       Mn	Mimimum Exposure
>       No	No Exposure
>       NA	No Basement
>
>BsmtFinType1: Rating of basement finished area（地下室完工面积评级）
>
>       GLQ	Good Living Quarters
>       ALQ	Average Living Quarters
>       BLQ	Below Average Living Quarters	
>       Rec	Average Rec Room
>       LwQ	Low Quality
>       Unf	Unfinshed
>       NA	No Basement
>
>BsmtFinSF1: Type 1 finished square feet(地下室完成的面积)
>
>BsmtFinType2: Rating of basement finished area (if multiple types)(地下室完成比例)
>
>       GLQ	Good Living Quarters
>       ALQ	Average Living Quarters
>       BLQ	Below Average Living Quarters	
>       Rec	Average Rec Room
>       LwQ	Low Quality
>       Unf	Unfinshed
>       NA	No Basement
>
>BsmtFinSF2: Type 2 finished square feet
>
>BsmtUnfSF: Unfinished square feet of basement area
>
>TotalBsmtSF: Total square feet of basement area（地下室总面积）
>
>Heating: Type of heating（加热类型(暖气方面)）
>		
>       Floor	Floor Furnace
>       GasA	Gas forced warm air furnace
>       GasW	Gas hot water or steam heat
>       Grav	Gravity furnace	
>       OthW	Hot water or steam heat other than gas
>       Wall	Wall furnace
>
>HeatingQC: Heating quality and condition（加热质量）
>
>       Ex	Excellent
>       Gd	Good
>       TA	Average/Typical
>       Fa	Fair
>       Po	Poor
>
>CentralAir: Central air conditioning（中央空调）
>
>       N	No
>       Y	Yes
>
>Electrical: Electrical system（电力系统）
>
>       SBrkr	Standard Circuit Breakers & Romex
>       FuseA	Fuse Box over 60 AMP and all Romex wiring (Average)	
>       FuseF	60 AMP Fuse Box and mostly Romex wiring (Fair)
>       FuseP	60 AMP Fuse Box and mostly knob & tube wiring (poor)
>       Mix	Mixed
>
>1stFlrSF: First Floor square feet(第一层面积)
>
>2ndFlrSF: Second floor square feet
>
>LowQualFinSF: Low quality finished square feet (all floors)（质量差的成品平方英尺(所有地板)）
>
>GrLivArea: Above grade (ground) living area square feet（地面以上居住面积平方英尺）
>
>BsmtFullBath: Basement full bathrooms（地下室全浴室）
>
>BsmtHalfBath: Basement half bathrooms
>
>FullBath: Full bathrooms above grade（全高档浴室）
>
>HalfBath: Half baths above grade
>
>Bedroom: Bedrooms above grade (does NOT include basement bedrooms)(高档卧室)
>
>Kitchen: Kitchens above grade
>
>KitchenQual: Kitchen quality（粗放质量）
>
>       Ex	Excellent
>       Gd	Good
>       TA	Typical/Average
>       Fa	Fair
>       Po	Poor
>
>TotRmsAbvGrd: Total rooms above grade (does not include bathrooms)(高级房间数)
>
>Functional: Home functionality (Assume typical unless deductions are warranted)
>
>       Typ	Typical Functionality
>       Min1	Minor Deductions 1
>       Min2	Minor Deductions 2
>       Mod	Moderate Deductions
>       Maj1	Major Deductions 1
>       Maj2	Major Deductions 2
>       Sev	Severely Damaged
>       Sal	Salvage only
>
>Fireplaces: Number of fireplaces(壁炉个数)
>
>FireplaceQu: Fireplace quality
>
>       Ex	Excellent - Exceptional Masonry Fireplace
>       Gd	Good - Masonry Fireplace in main level
>       TA	Average - Prefabricated Fireplace in main living area or Masonry Fireplace in basement
>       Fa	Fair - Prefabricated Fireplace in basement
>       Po	Poor - Ben Franklin Stove
>       NA	No Fireplace
>
>GarageType: Garage location（车库位置）
>		
>       2Types	More than one type of garage
>       Attchd	Attached to home
>       Basment	Basement Garage
>       BuiltIn	Built-In (Garage part of house - typically has room above garage)
>       CarPort	Car Port
>       Detchd	Detached from home
>       NA	No Garage
>
>GarageYrBlt: Year garage was built（车库年份）
>		
>GarageFinish: Interior finish of the garage（车库内部完成情况）
>
>       Fin	Finished
>       RFn	Rough Finished	
>       Unf	Unfinished
>       NA	No Garage
>
>GarageCars: Size of garage in car capacity
>
>GarageArea: Size of garage in square feet
>
>GarageQual: Garage quality
>
>       Ex	Excellent
>       Gd	Good
>       TA	Typical/Average
>       Fa	Fair
>       Po	Poor
>       NA	No Garage
>
>GarageCond: Garage condition
>
>       Ex	Excellent
>       Gd	Good
>       TA	Typical/Average
>       Fa	Fair
>       Po	Poor
>       NA	No Garage
>
>PavedDrive: Paved driveway(私人车道情况)
>
>       Y	Paved 
>       P	Partial Pavement
>       N	Dirt/Gravel
>
>WoodDeckSF: Wood deck area in square feet（木甲板面积）
>
>OpenPorchSF: Open porch area in square feet（开放门廊面积）
>
>EnclosedPorch: Enclosed porch area in square feet（封闭式门廊面积）
>
>3SsnPorch: Three season porch area in square feet（三季玄关面积平方英尺）
>
>ScreenPorch: Screen porch area in square feet（屏廊面积）
>
>PoolArea: Pool area in square feet（水池面积）
>
>PoolQC: Pool quality
>		
>       Ex	Excellent
>       Gd	Good
>       TA	Average/Typical
>       Fa	Fair
>       NA	No Pool
>
>Fence: Fence quality（栅栏面积）
>		
>       GdPrv	Good Privacy
>       MnPrv	Minimum Privacy
>       GdWo	Good Wood
>       MnWw	Minimum Wood/Wire
>       NA	No Fence
>
>MiscFeature: Miscellaneous feature not covered in other categories（其他类别中未涉及的杂项功能）
>		
>       Elev	Elevator
>       Gar2	2nd Garage (if not described in garage section)
>       Othr	Other
>       Shed	Shed (over 100 SF)
>       TenC	Tennis Court
>       NA	None
>
>MiscVal: $Value of miscellaneous feature（杂项特征的价值）
>
>MoSold: Month Sold (MM)(月销量)
>
>YrSold: Year Sold (YYYY)（年销量）
>
>SaleType: Type of sale(售卖方式)
>		
>       WD 	Warranty Deed - Conventional
>       CWD	Warranty Deed - Cash
>       VWD	Warranty Deed - VA Loan
>       New	Home just constructed and sold
>       COD	Court Officer Deed/Estate
>       Con	Contract 15% Down payment regular terms
>       ConLw	Contract Low Down payment and low interest
>       ConLI	Contract Low Interest
>       ConLD	Contract Low Down
>       Oth	Other
>
>SaleCondition: Condition of sale（售卖条件）
>
>       Normal	Normal Sale
>       Abnorml	Abnormal Sale -  trade, foreclosure, short sale
>       AdjLand	Adjoining Land Purchase
>       Alloca	Allocation - two linked properties with separate deeds, typically condo with a garage unit	
>       Family	Sale between family members
>       Partial	Home was not completed when last assessed (associated with New Homes)
>
>



以上使数据特征的简单标注，由于特征繁多，建议先可视化各个特征与目标的关系，然后选取明显特征作为分析对象
