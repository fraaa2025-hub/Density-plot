# Density-plot
############################################################
# 02_DensityPlot.R
# Density plot before and after filtering
############################################################

library(edgeR)
library(RColorBrewer)

# Raw data
lcpm.raw <- cpm(DGEList(counts = rawdata,
                        group = group),
                log = TRUE)

# Filtered data
lcpm.filtered <- cpm(y,
                     log = TRUE)

samplenames <- colnames(y)

nsamples <- ncol(y)

col <- brewer.pal(nsamples, "Paired")

par(mfrow = c(1,2))

plot(density(lcpm.raw[,1]),
     col = col[1],
     lwd = 2,
     ylim = c(0,0.21),
     main = "Raw Data",
     xlab = "Log-CPM")

for(i in 2:nsamples){
    lines(density(lcpm.raw[,i]),
          col = col[i],
          lwd = 2)
}

legend("topright",
       legend = samplenames,
       text.col = col,
       bty = "n")

plot(density(lcpm.filtered[,1]),
     col = col[1],
     lwd = 2,
     ylim = c(0,0.21),
     main = "Filtered Data",
     xlab = "Log-CPM")

for(i in 2:nsamples){
    lines(density(lcpm.filtered[,i]),
          col = col[i],
          lwd = 2)
}

legend("topright",
       legend = samplenames,
       text.col = col,
       bty = "n")
