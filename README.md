### Lesson Notes

```r
# 1. acquire data
beacukai <- read.csv("https://beacukai.go.id/datasource.csv", 
  header=FALSE,
  sep=";")
  
# 2. exploratory
head(beacukai, 7)
nrow(beacukai) # number of rows
ncol(beacukai) # number of columns
str(beacukai) # structure
summary(beacukai)
dim(beacukai)
names(beacukai)
length(names(beacukai))
length(unique(beacukai$port_id))

# 3. tabulation
# use `$` to specify a column
table1 <- table(beacukai$item.type, beacukai$port)
prop.table(table1) # in proportion
pie(table1)

# 4. cleansing
# head(beacukai$tax.declaration) -> 17.04.2021
beacukai$tax.declaration <- as.Date(
  beacukai$tax.declaration,
  format='%d.%m.%Y'
)

# 5. subset
cargo <- beacukai[6, 10:15]
cargo <- beacukai[beacukai$shipping == "cargo", ]
cargo <- beacukai[
            beacukai$shipping == "cargo" 
            & beacukai$arrival.date > as.Date("2022-01-31"), ]
cargo <- subset(beacukai, shipping == "cargo")

# 6. exploratory / early analysis / hypothesis
xtabs(formula, data)
xtabs(item.value ~ ship.mode, beacukai)
xtabs(item.value ~ declaration_form_method + cargo.size, cargo)
```
