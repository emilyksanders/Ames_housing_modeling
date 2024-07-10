# **Real Estate: It's Ame-azing!**
### *A report on predicting the sales price of houses in Ames, Iowa.*
###### Emily K. Sanders, DSB-318, April 19, 2024
---

<img src='https://git.generalassemb.ly/eksanders/Sanders_DSB318_Project_2/blob/ec9d60819607e4f9d2e853958f1e3e1df2918c23/images/duffy-house.png'>

###### A house in Ames, Iowa. Source: [Zillow](https://www.zillow.com/homedetails/1615-Duff-Ave-Ames-IA-50010/115840126_zpid/)

## Problem Statement
The housing market in Ames, Iowa is [small but competitive](https://www.redfin.com/city/477/IA/Ames/housing-market), and houses often go quickly (Redfin, 2024).  In such a market, realtors and their clients can gain advantage by correctly estimating how much a house will sell for, whether the client is buying or selling.  In this report, I will produce and explain a model that realtors can use to make this estimate.  As a secondary goal, I will look for elements of a house that contribute greatly to its value, to give sellers some ideas of how to improve their home's resale value.

### Deliverables
- Primary: **A model calibrated to predict home sale prices**, as assessed through *R-squared* and *Root Mean Square Error*.
- Secondary: **Recommendations to sellers on which elements of their homes to invest in,** based on the best conclusions I can draw from the interpretation of my models.  

### Audience
I have been contracted by the Greater Ames Realtor Licensees of Iowa Coalition to produce this model for their members, real estate agents in the Ames area.  The primary goal is to create a model that can be run easily on their computers, with no specialized knowledge on their part, so that they can get estimates of the prices of houses their clients are trying to buy or sell.  The recommendations, if any, that comprise my secondary goal will be delivered in writing only.

## Method
The commissioners of this project provided me with a dataset that was orignally compiled by the Ames City Assessor's office, that contains nearly 80 columns of information about 2051 home sales in Ames between 2006 and 2010.  Using this dataset I will develop and test several linear models to predict the sales price of a house its attributes,  This model must be reproducible without extensive hands-on data cleaning, as per the needs of my clients.

A data dictionary is provided at the bottom of this readme.

## Results
<img src='https://git.generalassemb.ly/eksanders/Sanders_DSB318_Project_2/blob/ec9d60819607e4f9d2e853958f1e3e1df2918c23/images/sale-price-histogram.png'>
The distribution of home prices in the dataset can be seen above.  Skewed data such as these - with a tail extending assymetrically towards the right - can be difficult to model well with linear techniques, but this is not always catastrophically detrimental.  

My most successful model was a LASSO regression with alpha of 1.  When tested on novel data, this model accounted for approximately 92% of the variation in home prices (*R-squared*), and made predictions with an average distance of +/-\$22,695.24 from the true price (*RMSE*).  This is a sizable improvement over the current baseline model, which averages a distance of \$79,975.12.  

To assess the quality of this model, I additionally plotted the residuals - the distance between the actual price and the predicted price.  In an ideal model, these residuals would form a bell curve centered on zero.  As can be seen in the graph below, the residuals of my LASSO model, while not perfectly curve-shaped or symmetrical, are approximatey centered on 0, and form a rough bell shape.  This is a very promising sign for the model's integrity and utility.

<img src='https://git.generalassemb.ly/eksanders/Sanders_DSB318_Project_2/blob/main/images/resids-hist.png'>

*Residuals are more or less normally distributed with a mean of 0.*

## Conclusions
The LASSO model I produced offers considerable advantage over other tools currently available to my clients, and I look forward to deploying it to them.  It offers solid predictive power for the price a house will sell for, and will allow my clients to help their clients make financially sound real estate decisions.  Unfortunately though, because LASSO regression results in uninterpretable coefficients, and because my interpretable models did not offer satisfactory *R-squared* or *RMSE*, I am unable to provide recommendations for improving a house's value at this time.  I will revisit this issue, as well as further fine tune the predictive power of the model, in future iterations of this project.


## Data Dictionary
The data dictionary below provides a guide to all the variable names in the dataset, as well as all the levels each categorical variable can take on.  They are presented here under the names I assigned to them, but much of the language here is taken verbatim from the [data dictionary](https://www.kaggle.com/competitions/318-ames-competition/data) that accompanied the dataset I received.

| Variable Name         | Type                      | Levels      | Explanation                                                                            |
| --------------------- | ------------------------- | ----------- | -------------------------------------------------------------------------------------- |
| saleprice             | int                       |             | the property's sale price in dollars                                                   |
| id                    | (for reference only) |             | short ID number                                                                        |
| pid                   | (for reference only) |             | long ID number                                                                         |
| building_type         | categorical               |             | building class                                                                         |
|                       |                           | 20          | 1-story 1946 & newer all styles                                                        |
|                       |                           | 30          | 1-story 1945 & older                                                                   |
|                       |                           | 40          | 1-story w/finished attic all ages                                                      |
|                       |                           | 45          | 1-1/2 story - unfinished all ages                                                      |
|                       |                           | 50          | 1-1/2 story finished all ages                                                          |
|                       |                           | 60          | 2-story 1946 & newer                                                                   |
|                       |                           | 70          | 2-story 1945 & older                                                                   |
|                       |                           | 75          | 2-1/2 story all ages                                                                   |
|                       |                           | 80          | split or multi-level                                                                   |
|                       |                           | 85          | split foyer                                                                            |
|                       |                           | 90          | duplex - all styles and ages                                                           |
|                       |                           | 120         | 1-story PUD - 1946 & newer                                                             |
|                       |                           | 150         | 1-1/2 story PUD - all ages                                                             |
|                       |                           | 160         | 2-story PUD - 1946 & newer                                                             |
|                       |                           | 180         | PUD - multilevel - incl split lev/foyer                                                |
|                       |                           | 190         | 2 family conversion - all styles and ages                                              |
| zoning                | categorical               |             | general zoning classification of the sale                                              |
|                       |                           | A (agr)     | agriculture                                                                            |
|                       |                           | C (all)     | commercial                                                                             |
|                       |                           | FV          | floating village residential                                                           |
|                       |                           | I (all)     | industrial                                                                             |
|                       |                           | RH          | residential high density                                                               |
|                       |                           | RL          | residential low density                                                                |
|                       |                           | RP          | residential low density park                                                           |
|                       |                           | RM          | residential medium density                                                             |
| lot_frontage          | float                     |             | linear feet of street connected to property                                            |
| lot_area              | int                       |             | lot size in square feet                                                                |
| street                | categorical               |             | type of road access to property                                                        |
|                       |                           | Grvl        | gravel                                                                                 |
|                       |                           | Pave        | paved                                                                                  |
| alley                 | categorical               |             | type of alley access to property                                                       |
|                       |                           | Grvl        | gravel                                                                                 |
|                       |                           | Pave        | paved                                                                                  |
|                       |                           | not-present | no alley access                                                                        |
| lot_shape             | categorical               |             | general shape of property                                                              |
|                       |                           | Reg         | Regular                                                                                |
|                       |                           | IR1         | Slightly irregular                                                                     |
|                       |                           | IR2         | Moderately Irregular                                                                   |
|                       |                           | IR3         | Irregular                                                                              |
| land_contour          | categorical               |             | flatness of the property                                                               |
|                       |                           | Lvl         | Near Flat/Level                                                                        |
|                       |                           | Bnk         | Banked - Quick and significant rise from street grade to building                      |
|                       |                           | HLS         | Hillside - Significant slope from side to side                                         |
|                       |                           | Low         | Depression                                                                             |
| utilities_type        | categorical               |             | type of utilities available                                                            |
|                       |                           | AllPub      | All public Utilities (E,G,W,& S)                                                       |
|                       |                           | NoSewr      | Electricity, Gas, and Water (Septic Tank)                                              |
|                       |                           | NoSeWa      | Electricity and Gas Only                                                               |
|                       |                           | ELO         | Electricity only                                                                       |
| lot_config            | categorical               |             | lot configuration                                                                      |
|                       |                           | Inside      | inside lot                                                                             |
|                       |                           | Corner      | corner lot                                                                             |
|                       |                           | CulDSac     | cul-de-sac                                                                             |
|                       |                           | FR2         | frontage on 2 sides of property                                                        |
|                       |                           | FR3         | frontage on 3 sides of property                                                        |
| land_slope            | categorical               |             | slope of property                                                                      |
|                       |                           | Gtl         | gentle slope                                                                           |
|                       |                           | Mod         | moderate Slope                                                                         |
|                       |                           | Sev         | severe Slope                                                                           |
| neighborhood          | categorical               |             | physical locations within Ames city limits                                             |
|                       |                           | Blmngtn     | Bloomington Heights                                                                    |
|                       |                           | Blueste     | Bluestem                                                                               |
|                       |                           | BrDale      | Briardale                                                                              |
|                       |                           | BrkSide     | Brookside                                                                              |
|                       |                           | ClearCr     | Clear Creek                                                                            |
|                       |                           | CollgCr     | College Creek                                                                          |
|                       |                           | Crawfor     | Crawford                                                                               |
|                       |                           | Edwards     | Edwards                                                                                |
|                       |                           | Gilbert     | Gilbert                                                                                |
|                       |                           | IDOTRR      | Iowa DOT and Rail Road                                                                 |
|                       |                           | MeadowV     | Meadow Village                                                                         |
|                       |                           | Mitchel     | Mitchell                                                                               |
|                       |                           | Names       | North Ames                                                                             |
|                       |                           | NoRidge     | Northridge                                                                             |
|                       |                           | NPkVill     | Northpark Villa                                                                        |
|                       |                           | NridgHt     | Northridge Heights                                                                     |
|                       |                           | NWAmes      | Northwest Ames                                                                         |
|                       |                           | OldTown     | Old Town                                                                               |
|                       |                           | SWISU       | South & West of Iowa State University                                                  |
|                       |                           | Sawyer      | Sawyer                                                                                 |
|                       |                           | SawyerW     | Sawyer West                                                                            |
|                       |                           | Somerst     | Somerset                                                                               |
|                       |                           | StoneBr     | Stone Brook                                                                            |
|                       |                           | Timber      | Timberland                                                                             |
|                       |                           | Veenker     | Veenker                                                                                |
| prox_to_road_rr_1     | categorical               |             | proximity to main road or railroad                                                     |
|                       |                           | Artery      | adjacent to arterial street                                                            |
|                       |                           | Feedr       | adjacent to feeder street                                                              |
|                       |                           | Norm        | normal                                                                                 |
|                       |                           | RRNn        | within 200' of North-South Railroad                                                    |
|                       |                           | RRAn        | adjacent to North-South Railroad                                                       |
|                       |                           | PosN        | near positive off-site feature--park, greenbelt, etc.                                  |
|                       |                           | PosA        | adjacent to postive off-site feature                                                   |
|                       |                           | RRNe        | within 200' of East-West Railroad                                                      |
|                       |                           | RRAe        | adjacent to East-West Railroad                                                         |
| prox_to_road_rr_2     | categorical               |             | proximity to second main road or railroad, if present                                  |
|                       |                           | Artery      | adjacent to arterial street                                                            |
|                       |                           | Feedr       | adjacent to feeder street                                                              |
|                       |                           | Norm        | normal                                                                                 |
|                       |                           | RRNn        | within 200' of North-South Railroad                                                    |
|                       |                           | RRAn        | adjacent to North-South Railroad                                                       |
|                       |                           | PosN        | near positive off-site feature--park, greenbelt, etc.                                  |
|                       |                           | PosA        | adjacent to postive off-site feature                                                   |
|                       |                           | RRNe        | within 200' of East-West Railroad                                                      |
|                       |                           | RRAe        | adjacent to East-West Railroad                                                         |
| bldg_type             | categorical               |             | type of dwelling                                                                       |
|                       |                           | 1Fam        | single-family detached                                                                 |
|                       |                           | 2FmCon      | two-family conversion; originally built as one-family dwelling                         |
|                       |                           | Duplx       | duplex                                                                                 |
|                       |                           | TwnhsE      | townhouse end unit                                                                     |
|                       |                           | TwnhsI      | townhouse inside unit                                                                  |
| house_style           | categorical               |             | style of dwelling                                                                      |
|                       |                           | 1Story      | one story                                                                              |
|                       |                           | 1.5Fin      | one and one-half story: 2nd level finished                                             |
|                       |                           | 1.5Unf      | one and one-half story: 2nd level unfinished                                           |
|                       |                           | 2Story      | two story                                                                              |
|                       |                           | 2.5Fin      | two and one-half story: 2nd level finished                                             |
|                       |                           | 2.5Unf      | two and one-half story: 2nd level unfinished                                           |
|                       |                           | SFoyer      | split foyer                                                                            |
|                       |                           | SLvl        | split level                                                                            |
| overall_qual          | ordinal                   |             | overall material and finish quality                                                    |
|                       |                           | 9          | very excellent                                                                         |
|                       |                           | 8           | excellent                                                                              |
|                       |                           | 7           | very good                                                                              |
|                       |                           | 6           | good                                                                                   |
|                       |                           | 5           | above average                                                                          |
|                       |                           | 4           | average                                                                                |
|                       |                           | 3           | below average                                                                          |
|                       |                           | 2           | fair                                                                                   |
|                       |                           | 1           | poor                                                                                   |
|                       |                           | 0           | very poor                                                                              |
| overall_cond          | ordinal                   |             | overall condition rating                                                               |
|                       |                           | 9          | very excellent                                                                         |
|                       |                           | 8           | excellent                                                                              |
|                       |                           | 7           | very good                                                                              |
|                       |                           | 6           | good                                                                                   |
|                       |                           | 5           | above average                                                                          |
|                       |                           | 4           | average                                                                                |
|                       |                           | 3           | below average                                                                          |
|                       |                           | 2           | fair                                                                                   |
|                       |                           | 1           | poor                                                                                   |
|                       |                           | 0           | very poor                                                                              |
| year_built            | int                       |             | original construction date                                                             |
| year_remodel_add      | int                       |             | remodel or addition date (same as construction date if none)                           |
| roof_style            | categorical               |             | type of roof                                                                           |
|                       |                           | Flat        | flat                                                                                   |
|                       |                           | Gable       | gable                                                                                  |
|                       |                           | Gambrel     | gabrel (barn)                                                                          |
|                       |                           | Hip         | hip                                                                                    |
|                       |                           | Mansard     | mansard                                                                                |
|                       |                           | Shed        | shed                                                                                   |
| roof_material         | categorical               |             | roof material                                                                          |
|                       |                           | ClyTile     | clay or tile                                                                           |
|                       |                           | CompShg     | standard (composite) shingle                                                           |
|                       |                           | Membran     | membrane                                                                               |
|                       |                           | Metal       | metal                                                                                  |
|                       |                           | Roll        | roll                                                                                   |
|                       |                           | Tar&Grv     | gravel & tar                                                                           |
|                       |                           | WdShake     | wood shakes                                                                            |
|                       |                           | WdShngl     | wood shingles                                                                          |
| exterior_1            | categorical               |             | exterior covering on house                                                             |
|                       |                           | AsbShng     | asbestos shingles                                                                      |
|                       |                           | AsphShn     | asphalt shingles                                                                       |
|                       |                           | BrkComm     | brick common                                                                           |
|                       |                           | BrkFace     | brick face                                                                             |
|                       |                           | CBlock      | cinder block                                                                           |
|                       |                           | CemntBd     | cement board                                                                           |
|                       |                           | HdBoard     | hard board                                                                             |
|                       |                           | ImStucc     | imitation stucco                                                                       |
|                       |                           | MetalSd     | metal siding                                                                           |
|                       |                           | Other       | other                                                                                  |
|                       |                           | Plywood     | plywood                                                                                |
|                       |                           | PreCast     | precast                                                                                |
|                       |                           | Stone       | stone                                                                                  |
|                       |                           | Stucco      | stucco                                                                                 |
|                       |                           | VinylSd     | vinyl siding                                                                           |
|                       |                           | Wd Sdng     | wood siding                                                                            |
|                       |                           | WdShing     | wood shingles                                                                          |
| exterior_2            | categorical               |             | second exterior covering on house if present                                           |
|                       |                           | AsbShng     | asbestos shingles                                                                      |
|                       |                           | AsphShn     | asphalt shingles                                                                       |
|                       |                           | BrkComm     | brick common                                                                           |
|                       |                           | BrkFace     | brick face                                                                             |
|                       |                           | CBlock      | cinder block                                                                           |
|                       |                           | CemntBd     | cement board                                                                           |
|                       |                           | HdBoard     | hard board                                                                             |
|                       |                           | ImStucc     | imitation stucco                                                                       |
|                       |                           | MetalSd     | metal siding                                                                           |
|                       |                           | Other       | other                                                                                  |
|                       |                           | Plywood     | plywood                                                                                |
|                       |                           | PreCast     | precast                                                                                |
|                       |                           | Stone       | stone                                                                                  |
|                       |                           | Stucco      | stucco                                                                                 |
|                       |                           | VinylSd     | vinyl siding                                                                           |
|                       |                           | Wd Sdng     | wood siding                                                                            |
|                       |                           | WdShing     | wood shingles                                                                          |
| masonry_type          | categorical               |             | masonry veneer type                                                                    |
|                       |                           | BrkComm     | brick common                                                                           |
|                       |                           | BrkFace     | brick face                                                                             |
|                       |                           | CBlock      | cinder block                                                                           |
|                       |                           | Stone       | stone                                                                                  |
|                       |                           | not-present | none                                                                                   |
| masonry_area          | float                     |             | masonry veneer area in square feet                                                     |
| exter_qual            | ordinal                   |             | exterior material quality                                                              |
|                       |                           | Ex          | excellent                                                                              |
|                       |                           | Gd          | good                                                                                   |
|                       |                           | TA          | average/typical                                                                        |
|                       |                           | Fa          | fair                                                                                   |
|                       |                           | Po          | poor                                                                                   |
| exter_cond            | ordinal                   |             | present condition of the material on the exterior                                      |
|                       |                           | Ex          | excellent                                                                              |
|                       |                           | Gd          | good                                                                                   |
|                       |                           | TA          | average/typical                                                                        |
|                       |                           | Fa          | fair                                                                                   |
|                       |                           | Po          | poor                                                                                   |
| foundation            | categorical               |             | type of foundation                                                                     |
|                       |                           | BrkTil      | brick & tile                                                                           |
|                       |                           | CBlock      | cinder block                                                                           |
|                       |                           | PConc       | poured contrete                                                                        |
|                       |                           | Slab        | slab                                                                                   |
|                       |                           | Stone       | stone                                                                                  |
|                       |                           | Wood        | wood                                                                                   |
| basemt_qual           | ordinal                   |             | height of the basement                                                                 |
|                       |                           | Ex          | excellent (100+ inches)                                                                |
|                       |                           | Gd          | good (90-99 inches)                                                                    |
|                       |                           | TA          | typical (80-89 inches)                                                                 |
|                       |                           | Fa          | fair (70-79 inches)                                                                    |
|                       |                           | Po          | poor (<70 inches)                                                                      |
|                       |                           | not-present | no Basement                                                                            |
| basemt_cond           | ordinal                   |             | general condition of the basement                                                      |
|                       |                           | Ex          | excellent                                                                              |
|                       |                           | Gd          | good                                                                                   |
|                       |                           | TA          | typical - slight dampness allowed                                                      |
|                       |                           | Fa          | fair - dampness or some cracking or settling                                           |
|                       |                           | Po          | poor - severe cracking, settling, or wetness                                           |
|                       |                           | NA          | no basement                                                                            |
| basemt_exposure       | ordinal                   |             | walkout or garden level basement walls                                                 |
|                       |                           | Gd          | good exposure                                                                          |
|                       |                           | Av          | average exposure (split levels or foyers typically score average or above)             |
|                       |                           | Mn          | mimimum exposure                                                                       |
|                       |                           | No          | no exposure                                                                            |
|                       |                           | NA          | no basement                                                                            |
| basemt_fin_1_qual     | ordinal                   |             | quality of finished area in the basement                                               |
|                       |                           | GLQ         | good living quarters                                                                   |
|                       |                           | ALQ         | average living quarters                                                                |
|                       |                           | BLQ         | below average living quarters                                                          |
|                       |                           | Rec         | average rec room                                                                       |
|                       |                           | LwQ         | low quality                                                                            |
|                       |                           | Unf         | unfinshed                                                                              |
|                       |                           | not-present | no basement                                                                            |
| basemt_fin_1_sf       | float                     |             | square feet of finished area in basement                                               |
| basemt_fin_2_qual     | ordinal                   |             | quality of second finished area in the basement if present                             |
|                       |                           | GLQ         | good living quarters                                                                   |
|                       |                           | ALQ         | average living quarters                                                                |
|                       |                           | BLQ         | below average living quarters                                                          |
|                       |                           | Rec         | average rec room                                                                       |
|                       |                           | LwQ         | low quality                                                                            |
|                       |                           | Unf         | unfinshed                                                                              |
|                       |                           | not-present | no basement                                                                            |
| basemt_fin_2_sf       | float                     |             | square feet of second finished area in basement if present                             |
| basemt_unf_sf         | float                     |             | square feet of unfinished area in basement                                             |
| basemt_total_sf       | float                     |             | total square feet of basement area                                                     |
| heating               | categorical               |             | type of heating                                                                        |
|                       |                           | Floor       | floor furnace                                                                          |
|                       |                           | GasA        | gas forced warm air furnace                                                            |
|                       |                           | GasW        | gas hot water or steam heat                                                            |
|                       |                           | Grav        | gravity furnace                                                                        |
|                       |                           | OthW        | hot water or steam heat other than gas                                                 |
|                       |                           | Wall        | wall furnace                                                                           |
| heating_qc            | ordinal                   |             | heating quality and condition                                                          |
|                       |                           | Ex          | excellent                                                                              |
|                       |                           | Gd          | good                                                                                   |
|                       |                           | TA          | average/typical                                                                        |
|                       |                           | Fa          | fair                                                                                   |
|                       |                           | Po          | poor                                                                                   |
| central_air           | binary                    |             | presence of central air conditioning                                                   |
|                       |                           | N           | no                                                                                     |
|                       |                           | Y           | yes                                                                                    |
| electrical            | categorical               |             | type of electrical system                                                              |
|                       |                           | SBrkr       | standard circuit breakers & Romex                                                      |
|                       |                           | FuseA       | fuse box over 60 amp and all Romex wiring (average)                                    |
|                       |                           | FuseF       | 60 amp fuse box and mostly Romex wiring (fair)                                         |
|                       |                           | FuseP       | 60 amp fuse box and mostly knob & tube wiring (poor)                                   |
|                       |                           | Mix         | mixed                                                                                  |
| floor_1_sf            | float                     |             | square feet of first floor                                                             |
| floor_2_sf            | float                     |             | square feet of second floor                                                            |
| low_qual_fin_sf       | float                     |             | square feet of low quality finished area (all floors)                                  |
| gr_liv_area           | float                     |             | square feet of above-ground living area                                                |
| basemt_full_bath      | int                       |             | number of basement full bathrooms                                                      |
| basemt_half_bath      | int                       |             | number of basement half bathrooms                                                      |
| full_bath             | int                       |             | number of full bathrooms above ground                                                  |
| half_bath             | int                       |             | number of half bathrooms above ground                                                  |
| bedroom_abvgr         | int                       |             | number of bedrooms above basement level                                                |
| kitchen_abvgr         | int                       |             | number of kitchens                                                                     |
| kitchen_qual          | ordinal                   |             | kitchen quality                                                                        |
|                       |                           | Ex          | excellent                                                                              |
|                       |                           | Gd          | good                                                                                   |
|                       |                           | TA          | average/typical                                                                        |
|                       |                           | Fa          | fair                                                                                   |
|                       |                           | Po          | poor                                                                                   |
| total_rms_abv_grd     | int                       |             | total rooms above grade (not including bathrooms)                                      |
| home_functionality    | ordinal                   |             | home functionality rating                                                              |
|                       |                           | Typ         | typical functionality                                                                  |
|                       |                           | Min1        | minor deductions 1                                                                     |
|                       |                           | Min2        | minor deductions 2                                                                     |
|                       |                           | Mod         | moderate deductions                                                                    |
|                       |                           | Maj1        | major deductions 1                                                                     |
|                       |                           | Maj2        | major deductions 2                                                                     |
|                       |                           | Sev         | severely damaged                                                                       |
|                       |                           | Sal         | salvage only                                                                           |
| fireplaces            | int                       |             | number of fireplaces                                                                   |
| fireplace_qu          | ordinal                   |             | FireplaceQu: Fireplace quality                                                         |
|                       |                           | Ex          | excellent - exceptional masonry fireplace                                              |
|                       |                           | Gd          | good - masonry fireplace in main level                                                 |
|                       |                           | TA          | average - prefabricated fireplace in main living area or masonry fireplace in basement |
|                       |                           | Fa          | fair - prefabricated fireplace in basement                                             |
|                       |                           | Po          | poor - ben franklin stove                                                              |
|                       |                           | not-present | no fireplace                                                                           |
| garage_type           | categorical               |             | garage location                                                                        |
|                       |                           | 2Types      | more than one type of garage                                                           |
|                       |                           | Attchd      | attached to home                                                                       |
|                       |                           | Basment     | basement garage                                                                        |
|                       |                           | BuiltIn     | built-in (garage part of house - typically has room above garage)                      |
|                       |                           | CarPort     | car port                                                                               |
|                       |                           | Detchd      | detached from home                                                                     |
|                       |                           | not-present | no garage                                                                              |
| garage_yr_blt         | int                       |             | year garage was built                                                                  |
| garage_finish         | categorical               |             | interior finish of the garage                                                          |
|                       |                           | Fin         | finished                                                                               |
|                       |                           | RFn         | rough finished                                                                         |
|                       |                           | Unf         | unfinished                                                                             |
|                       |                           | not-present | no garage                                                                              |
| garage_cars           | float                     |             | size of garage in car capacity                                                         |
| garage_area           | float                     |             | square feet of garage                                                                  |
| garage_qual           | ordinal                   |             | garage quality                                                                         |
|                       |                           | Ex          | excellent                                                                              |
|                       |                           | Gd          | good                                                                                   |
|                       |                           | TA          | average/typical                                                                        |
|                       |                           | Fa          | fair                                                                                   |
|                       |                           | Po          | poor                                                                                   |
|                       |                           | not-present | no garage                                                                              |
| garage_cond           | ordinal                   |             | garage condition                                                                       |
|                       |                           | Ex          | excellent                                                                              |
|                       |                           | Gd          | good                                                                                   |
|                       |                           | TA          | average/typical                                                                        |
|                       |                           | Fa          | fair                                                                                   |
|                       |                           | Po          | poor                                                                                   |
|                       |                           | not-present | no garage                                                                              |
| paved_drive           | categorical               |             | paved driveway                                                                         |
|                       |                           | Y           | paved                                                                                  |
|                       |                           | P           | partially paved                                                                        |
|                       |                           | N           | not paved - dirt/gravel                                                                |
| wood_deck_sf          | float                     |             | square feet of wood deck area                                                          |
| open_porch_sf         | float                     |             | square feet of open porch area                                                         |
| encl_porch_sf         | float                     |             | square feet of enclosed porch area                                                     |
| three_season_porch_sf | float                     |             | square feet of three-season porch area                                                 |
| screen_porch_sf       | float                     |             | square feet of screened-in porch area                                                  |
| pool_area             | float                     |             | square feet of pool area                                                               |
| pool_qc               | ordinal                   |             | pool quality                                                                           |
|                       |                           | Ex          | excellent                                                                              |
|                       |                           | Gd          | good                                                                                   |
|                       |                           | TA          | average/typical                                                                        |
|                       |                           | Fa          | fair                                                                                   |
|                       |                           | not-present | no pool                                                                                |
| fence                 | categorical               |             | fence quality                                                                          |
|                       |                           | GdPrv       | good privacy                                                                           |
|                       |                           | MnPrv       | minimum privacy                                                                        |
|                       |                           | GdWo        | good wood                                                                              |
|                       |                           | MnWw        | minimum wood/wire                                                                      |
|                       |                           | not-present | no fence                                                                               |
| misc_feature          | categorical               |             | miscellaneous element of the house not covered in other categories                     |
|                       |                           | Elev        | elevator                                                                               |
|                       |                           | Gar         | 2nd garage (if not described in garage section)                                        |
|                       |                           | Othr        | other                                                                                  |
|                       |                           | Shed        | shed (over 100 sf)                                                                     |
|                       |                           | TenC        | tennis court                                                                           |
|                       |                           | not-present | no extra elements                                                                      |
| misc_val              | int                       |             | monetary value of miscellaneous feature                                                |
| month_sold            | categorical               |             | month sold, represented numerically                                                    |
| yr_sold               | int                       |             | year sold, scaled to 2006=0                                                            |
| sale_type             | categorical               |             | type of sale                                                                           |
|                       |                           | WD          | warranty deed - conventional                                                           |
|                       |                           | CWD         | warranty deed - cash                                                                   |
|                       |                           | VWD         | warranty deed - va loan                                                                |
|                       |                           | New         | new home just constructed and sold                                                     |
|                       |                           | COD         | court officer deed/estate                                                              |
|                       |                           | Con         | contract 15% down payment regular terms                                                |
|                       |                           | ConLw       | contract low down payment and low interest                                             |
|                       |                           | ConLI       | contract low interest                                                                  |
|                       |                           | ConLD       | contract low down                                                                      |
|                       |                           | Oth         | other                                                                                  |
###### *Author's Note: I would like to express my gratitude to John Franey for his creation and maintenance of _[Table to Markdown](https://tabletomarkdown.com/)_, which made the creation of this sizeable table immeasurably easier, and for graciously making this tool available for free (2024).*







