# Testing AI Political Bias in Germany: A Replication Study using Synthetic Voter Profiles
This project asks whether large language models exhibit systematic partisan bias when
advising voters in non-English-speaking democracies. As AI chatbots increasingly serve as intermediaries for
political information, we want to test how models handle political advice in the German context. 

## Methodology
The approach is largely based on Miyazaki & Hall (2026) who evaluated party recommendations in a Japanese context.

We present each model with standardized German/English prompts asking for a
party recommendation based on the synthetic profiles (demographics, policy stances).
We use text processing (Regex) to extract the recommended party names and apply
OLS regressions to measure the exact effect of each demographic variable and policy stance on the probability
of a specific party being recommended.

### References
Miyazaki & Hall, ”Why Do AI Models Tell Left-Wing Voters to Support the Communist
Party? AI Voting Advice in Japan’s 2026 General Election” (2026), Working Paper
