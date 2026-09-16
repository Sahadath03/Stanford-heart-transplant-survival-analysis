# Stanford-heart-transplant-survival-analysis

Project Overview 

This project analyzes survival outcomes from the Stanford Heart Transplant study to investigate whether receiving a heart transplant was associated with improved survival and to identify factors associated with mortality risk.

The analysis was conducted as part of graduate-level Survival Analysis coursework using R.

Research Questions

- Is receiving a heart transplant associated with improved survival?
- Does age influence survival outcomes?
- Does acceptance year influence survival?
- Among transplant recipients, do prior surgery and antigen mismatch
  influence survival?
- Do the effects of transplant differ by age group?
  
Dataset
The dataset contains 103 patient observations and includes variables such as:

- Patient ID
- Age
- Acceptance year
- Survival status
- Survival time
- Prior surgery
- Transplant status
- Waiting time
- Antigen mismatch


library(survival)
data(heart, package="survival")
data



Statistical Methods

The following methods were used:

- Kaplan-Meier survival analysis
- Log-rank tests
- Cox proportional hazards regression
- Multivariable Cox regression
- Weibull regression
- Likelihood-ratio tests
- Akaike Information Criterion (AIC)
- Proportional hazards assumption testing
- Residual diagnostics
- Sensitivity analysis

Key Findings

The analysis identified transplant status and age group as important predictors of survival.

The final Cox model included:
- Transplant status
- Age group
  
Model selection using AIC supported the model containing both transplant
status and age group.

A sensitivity analysis was also conducted after removing influential
observations to evaluate the stability of the results.

Model Diagnostics

The project included:

- Proportional hazards assumption testing
- Case-deletion residual analysis
- Identification of influential observations
- Sensitivity analysis after removal of influential observations

 Tools
- R
- RStudio

  Code
  
- Kaplan–Meier Curve by Treatment Group
  
# Install packages if needed
install.packages("survival")
install.packages("survminer")

# Load libraries
library(survival)
library(survminer)

# Convert data to proper factors
data$transplant <- factor(data$transplant, levels = c(0,1),
                          labels = c("Control", "Treatment"))

data$survived <- as.numeric(data$survived)  # 1 = event, 0 = censored

# Create survival object
surv_obj <- Surv(time = data$survtime, event = data$survived)

# Fit Kaplan–Meier model
fit <- survfit(surv_obj ~ transplant, data = data)

# Plot Kaplan–Meier curve
ggsurvplot(
  fit,
  data = data,
  pval = TRUE,                # display log-rank test p-value
  risk.table = TRUE,          # add risk table
  conf.int = TRUE,            # confidence intervals
  legend.title = "Group",
  legend.labs = c("Control", "Treatment"),
  xlab = "Time",
  ylab = "Survival probability",
  palette = "Dark2"           
)

- KM plots for each treatment group
# Control
fit_control <- survfit(Surv(survtime, survived) ~ prior, data = df_control)
ggsurvplot(fit_control, data=df_control, pval=TRUE, risk.table = TRUE)

# Treatment
fit_treatment <- survfit(Surv(survtime, survived) ~ prior, data = df_treatment)
ggsurvplot(fit_treatment, data=df_treatment, pval=TRUE, risk.table = TRUE)

- Log Rank Test
logrank_test <- survdiff(surv_obj ~ transplant, data = df)
logrank_test
