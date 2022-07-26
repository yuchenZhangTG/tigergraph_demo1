# TigerGraph demo on a cluster
Slide
https://docs.google.com/presentation/d/19mgHglhpRXOaefibprstugfNKlGuwbp_6b9TLS6sCN4/edit?usp=sharing

## Introduction
TigerGraph has two modes:
1. Non-distributed mode: the data is gethered at the local node. This mode targets for transaction workload (low latency for small query). 
2. Distributed mode: query is executed on all the nodes in parallel. This mode targets for analytical workload (large query that touch a large amount of data).

## Data schema and statistics
![alt text](./schema.png)
1T data: ~2.4 B vertices and ~17 B edges
| Comment  | Post | Person | Forum |
|-------|-------|-------|-------|
|1,876,785,283| 519,738,978 |  3,399,580 | 33,168,124 |

10T data: ~24 B vertices and ~173 B edges
| Comment  | Post | Person | Forum |
|-------|-------|-------|-------| 
|18,880,439,325| 4,461,342,990 |  26,384,952 | 257,338,738 |

## Results
### 1T LDBC SNB data
#### Environment
- 4x GCP n2d-highmem-64 
- Each machine has 64vCPU/512G RAM
- TigerGraph 3.7.0-RC

#### IS6 Latency (in millisecond) 
|CNT    |THEAD  |P50    |P90    |P95    |P99    |AVG    |QPS    |
|-------|-------|-------|-------|-------|-------|-------|-------|
|8000   |8      |26     |30     |31     |44     |27     |296    |
|16000  |16     |27     |31     |33     |45     |27     |590    |
|24000  |24     |32     |48     |52     |59     |35     |673    |
|32000  |32     |38     |62     |66     |86     |43     |721    |
|48000  |48     |58     |103    |121    |164    |66     |721    |
|64000  |64     |78     |157    |185    |253    |91     |694    |

#### IS2 Latency (in millisecond) 
|CNT    |THEAD  |P50    |P90    |P95    |P99    |AVG    |QPS    |
|-------|-------|-------|-------|-------|-------|-------|-------|
|8000   |8      |36     |46     |50     |57     |37     |210    |
|16000  |16     |39     |50     |55     |70     |40     |391    |
|24000  |24     |43     |57     |62     |79     |45     |529    |
|32000  |32     |51     |71     |77     |97     |54     |589    |
|48000  |48     |76     |102    |113    |134    |76     |622    |
|64000  |64     |97     |136    |149    |188    |100    |632    |

### 3T LDBC SNB data
#### Environment 
- 10x GCP n2d-highmem-64 
- Each machine has 64vCPU/512G RAM
- TigerGraph 3.7.0-RC

#### IS6 Latency (in millisecond) 
|CNT    |THEAD  |P50    |P90    |P95    |P99    |AVG    |QPS    |
|-------|-------|-------|-------|-------|-------|-------|-------|
|8000   |8      |58     |67     |69     |83     |59     |135    |
|16000  |16     |60     |69     |72     |96     |61     |262    |
|24000  |24     |60     |71     |74     |100    |60     |393    |
|32000  |32     |63     |76     |81     |112    |64     |492    |
|48000  |48     |72     |95     |127    |231    |78     |601    |
|64000  |64     |90     |153    |186    |333    |104    |608    |

#### IS2 Latency (in millisecond)
|CNT    |THEAD  |P50    |P90    |P95    |P99    |AVG    |QPS    |
|-------|-------|-------|-------|-------|-------|-------|-------|
|8000   |8      |73     |89     |95     |118    |75     |107    |
|16000  |16     |76     |92     |99     |125    |77     |204    |
|24000  |24     |77     |94     |101    |129    |79     |299    |
|32000  |32     |80     |100    |111    |152    |83     |379    |
|48000  |48     |91     |134    |168    |236    |100    |472    |
|64000  |64     |114    |198    |226    |329    |130    |485    |

### 10T LDBC SNB data
#### Environment 
- 20x GCP n2d-highmem-96 
- Each machine has 96vCPU/768G RAM
- TigerGraph 3.7.0-RC

#### IS6 Latency (in millisecond)
|CNT    |THEAD  |P50    |P90    |P95    |P99    |AVG    |QPS    |
|-------|-------|-------|-------|-------|-------|-------|-------|
|8000   |8      |137    |156    |172    |317    |143    |55     |
|16000  |16     |130    |150    |248    |360    |140    |112    |
|24000  |24     |131    |159    |308    |409    |143    |164    |
|32000  |32     |134    |318    |344    |431    |164    |190    |
|48000  |48     |142    |351    |373    |457    |205    |228    |
|64000  |64     |311    |373    |402    |475    |263    |238    |

#### IS2 Latency (in millisecond) 
|CNT    |THEAD  |P50    |P90    |P95    |P99    |AVG    |QPS    |
|-------|-------|-------|-------|-------|-------|-------|-------|
|8000   |8      |218    |310    |319    |350    |223    |35     |
|16000  |16     |264    |320    |332    |371    |234    |67     |
|24000  |24     |295    |331    |346    |395    |265    |89     |
|32000  |32     |308    |360    |379    |430    |275    |113    |
|48000  |48     |334    |392    |411    |471    |299    |157    |
|64000  |64     |352    |414    |437    |500    |318    |196    |