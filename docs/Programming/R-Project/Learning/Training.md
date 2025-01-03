

## Read excel

```r
# install.packages("readODS")
# install.packages("readxl")
readxl::excel_sheets("./2024_data_2nd.xlsx")
Site <- readxl::read_excel("./2024_data_2nd.xlsx", sheet = "Site")
Site$class_a
Site$class_a <- factor(Site$class_a, ordered = TRUE, 
                       levels = c("1987fire", "2000fire", "2024fire"))
Site$class_b <- factor(Site$class_b, ordered = FALSE)
summary(Site)

Soil_BD <- readxl::read_excel("./2024_data_2nd.xlsx", sheet = "Soil_BD")
mice::md.pattern(Soil_BD, rotate.names = TRUE) # 缺失值探索
Soil_BD_RE <- na.omit(Soil_BD[,c(1, 2, 3, 10, 11)])
Soil_BD_RE$Layer <- factor(Soil_BD_RE$Layer, ordered = TRUE,
                           levels = c("00_05", "05_15"))
Soil_BD_RE

Soil_OC <- readxl::read_excel("./2024_data_2nd.xlsx", sheet = "Soil_OC")
Soil_OC_RE <- na.omit(Soil_OC[,c(1,2,3,7)])
Soil_OC_RE

Orga_OC <- readxl::read_excel("./2024_data_2nd.xlsx", sheet = "Orga_OC")
Orga_OC_RE <- na.omit(Orga_OC[,c(1,2,3,7)])
Orga_OC_RE

library(tidyverse)
Orga_OC_SUM <- Orga_OC_RE %>% 
  group_by(., name, Layer) %>%
  summarise(TC = mean(`TC/g/kg`), TC_sd = sd(`TC/g/kg`))
Orga_OC_SUM

Soil_OC_SUM <- Soil_OC_RE %>%
  group_by(., name, Layer) %>%
  summarise(TC = mean(`TC/g/kg`), TC_sd = sd(`TC/g/kg`))
Soil_OC_SUM

OC <- rbind(Orga_OC_SUM, Soil_OC_SUM)
OC$Layer <- factor(OC$Layer, ordered = TRUE, 
                   levels = c("Litter", "Mattic", "00_05", "05_15"))
OC$name <- as.integer(OC$name)
OC <- arrange(OC, name, Layer)
# OC <- arrange(OC, name, desc(Layer)) # desc查看时倒序
# OC$Layer <- fct_rev(OC$Layer) # fct_rev 因子倒序
summary(OC)

# 含量的堆积柱状图，仅可视参考
ggplot(data = OC, aes(x = name, y = TC, fill = Layer)) + 
  geom_bar(
    stat = "identity", 
    position = "stack"
  )

ggplot(data = OC, aes(x = name, y = TC, colour = Layer, 
                      shape = Layer, linetype = Layer)) + 
  geom_point() + 
  geom_smooth(method = "lm")
```