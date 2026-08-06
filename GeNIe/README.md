# GeNIe Bayesian-network model and sensitivity analysis

This directory contains the GeNIe artifacts accompanying the manuscript
"An Interpretable Bayesian Network for Rotator Cuff Tear Risk Assessment in a
Large Cohort."

The final MMHC-based Bayesian network was implemented in GeNIe Modeler
(BayesFusion LLC, Pittsburgh, PA, USA) to support graphical inspection,
interactive posterior probability updating, and sensitivity analysis. The
GeNIe analyses complement the reproducible R workflow in the `analysis`
directory.

## Contents

The GeNIe network is distributed as an `.xdsl` model file in this directory.
The file contains the final directed acyclic graph, the discrete states of the
16 model nodes, and the learned conditional probability tables. It does not
contain participant-level UK Biobank records.

Any exported sensitivity plots or interface screenshots stored alongside the
model are derived from this GeNIe implementation.

## Analyses performed in GeNIe

GeNIe was used for the following analyses reported in the manuscript:

- visualization and inspection of the final MMHC-based Bayesian network;
- inspection of conditional probability tables;
- interactive posterior probability updating after entering evidence;
- one-way parameter sensitivity analysis for the probability of RCT;
- generation of the parameter-sensitivity tornado plot; and
- scenario-based probabilistic inference for illustrative patient profiles.

Parameter sensitivity analysis was conducted directly in GeNIe and is
therefore not recalculated by the R scripts in `analysis`. Evidence-sensitivity
and other programmatic analyses available in R are documented separately in
the main repository README.

## Opening the model

1. Download and install GeNIe Modeler from BayesFusion.
2. Download the `.xdsl` file in this directory.
3. Open GeNIe and select **File > Open**.
4. Select the downloaded `.xdsl` file.
5. Set `RCT` as the target node and use state `1` to represent recorded rotator
   cuff tear.

## Interactive probability updating

To reproduce an illustrative probability query:

1. Open the final network and confirm that no evidence is initially selected.
2. Record the marginal probability for `RCT = 1`.
3. Enter the required state for one or more evidence nodes.
4. Allow GeNIe to update the network and record the posterior probability for
   `RCT = 1`.
5. Clear all evidence before starting a new scenario.

Because inference is conditional on the complete set of entered evidence, the
posterior probability may differ when additional evidence is added or removed.

## Parameter sensitivity analysis

For the manuscript parameter-sensitivity analysis, `RCT = 1` was selected as
the target outcome. GeNIe's sensitivity-analysis function was then used to
evaluate how variation in the model parameters affected the estimated
probability of RCT. The resulting tornado plot ranks the parameters according
to the magnitude of their influence on the target probability.

The sensitivity output describes uncertainty within the fitted probabilistic
model. It should not be interpreted as evidence of a causal effect or as an
estimate of the effect of a clinical intervention.

## Node abbreviations

- `RCT`: rotator cuff tear
- `BMI`: body mass index
- `WH`: waist-to-hip ratio
- `DM`: diabetes mellitus
- `HP`: hyperlipidemia
- `HT`: hypertension
- `OP`: osteoporosis
- `BS`: subacromial bursitis
- `SIS`: shoulder impingement syndrome
- `AIF`: alcohol intake frequency
- `MA`: moderate physical activity
- `IMD`: Index of Multiple Deprivation
- `Work`: job involving heavy manual or physical work

## Interpretation and intended use

The network is intended for research, model inspection, and demonstration of
probabilistic risk assessment. Directed arcs represent conditional
dependencies in the fitted Bayesian network and should not be interpreted as
confirmed causal relationships. The model has undergone internal validation
but not external clinical validation and must not be used as a stand-alone
diagnostic tool or as the sole basis for referral, imaging, or treatment
decisions.

## Related analysis code

The R workflow is provided in:

1. `analysis/01_data_cleaning_and_multiple_imputation.R`
2. `analysis/02_bn_modeling_validation_and_figures.R`

Participant-level UK Biobank data are not included because of data-use and
privacy restrictions.
