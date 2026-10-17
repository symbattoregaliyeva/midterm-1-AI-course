# Midterm 1: answers

GitHub username: symbattoregaliyeva
Session code: MAPLE-66
Fingerprint: c3926e1a

> Fill in the three lines above from `my_data/DATA.md`. Do not rename headings or table columns: a script reads the numbers.
> Write only in the empty cells and lines. Percentages as 0.78 or 78 %, money as plain numbers.

## AI-use declaration

I used AI to understand the tasks and write code. Also I had to use it to explain my answers in English clearly

## Part 1: Retrieval and cost decision 

### 1a. Metrics (all 60 questions)

| config | recall@1 | recall@3 | recall@5 | MRR@10 |
|---|---|---|---|---|
| A | 0.63333333 | 0.83333333 | 0.88333333 | 0.72291667 |
| B | 0.33333333 | 0.53333333 | 0.76666667 | 0.47501984 |

### 1b. Recall and 95 % Wilson interval of each candidate (recall at its own k)

| candidate | recall@k | lower | upper |
|---|---|---|---|
| A, k=3 | 0.83333333 | 0.71968149 | 0.90686923 |
| A, k=5 | 0.88333333 | 0.77820979 | 0.94232353 |
| B, k=3 | 0.53333333 | 0.40893209 | 0.65372298 |
| B, k=5 | 0.76666667 | 0.64563489 | 0.85560568 |

### 1c. Annual model cost in USD

| candidate | annual cost |
|---|---|
| A, k=3 | 7229.83 |
| A, k=5 | 9814.92 |
| B, k=3 | 4302.89 |
| B, k=5 | 4936.70 |

### 1d. Decision (at most 150 words)

Chosen candidate: B  k=5

Choose B, k=5: annual cost 4936.70 is below the 8500 budget, leaving 3563.30. Recall is 46/60 = 76.67%, with Wilson interval [64.56%, 85.56%]. A, k=3 has higher observed recall, 83.33%, but its [71.97%, 90.69%] interval overlaps B, k=5; the course rule does not establish a winner between them. B, k=5 saves 2293.13 annually against A, k=3. A, k=5 costs 9814.92 and exceeds budget. Both A candidates have non-overlapping intervals with B, k=3 and higher recall; the remaining pairs overlap. B, k=5 is the cheapest affordable candidate whose interval overlaps the highest-recall affordable option. Its recall by language is EN 18/20 = 90%, RU 14/20 = 70%, and KK 14/20 = 70%. RU and KK are jointly worst served; KK represents 39% of production traffic.

### 1e. Next measurement (at most 60 words)
Evaluate B, k=5 and A, k=3 on 300 new, independently sampled questions: 100 per language, with verified relevant chunks. Report per-language recall and Wilson intervals, and assess answer correctness on the same questions. A demonstrated improvement, especially for RU or KK, could justify A, k=3's extra cost within the existing budget

## Part 2: A document pipeline you can defend

### 2a. Numbers

| pipeline | overall accuracy | weakest cell (language, condition) | accuracy there | lower | upper | annual cost |
|---|---|---|---|---|---|---|
| H | 0.85555556 | RU, clean | 0.73333333 | 0.55551698 | 0.85817504 | 43362.00 |
| L | 0.82777778 | RU, degraded | 0.73333333 | 0.55551698 | 0.85817504 | 32400.00 |
Personal-data pages per year sent abroad under H:295650

### 2b. Memo (at most 300 words)
To: Head of Operations

Choose L: it costs 32400 yearly versus 43362 for H. Test accuracy is 82.78% for L and 85.56% for H. H serves RU/clean scans worst; L serves RU/degraded worst. Both score 22/30 = 73.33%, with Wilson interval [55.55%, 85.82%]. These wide intervals show uncertainty, while overall averages hide weaker groups.

H sends scans abroad, including 295650 personal-data pages yearly. IIN is covered personal data under the course rules. We must confirm who stores images, outputs and logs, where backups go, and retention periods. A vendor statement is insufficient. L uses the bank’s servers in Kazakhstan, but administrator access, backups, telemetry and retention still need verification.

For L, use encryption, role-based access, audit logs and tested deletion rules. Block unapproved foreign transfers and check network logs. Send extraction failures to local human reviewers. Remaining risks include incorrect fields, weaker Russian-scan performance and outages: one failed server leaves capacity of 8000 pages/day against demand of 9000. Human review and safeguards add costs beyond the stated server budget.

## Part 3: Explain your own numbers

### Q1

Number:0.91
Why (at most 40 words):KK/EN ratios are 1.10 for characters, 2.13 for bytes and 1.95 for tokens. Tokens per byte are lower for KK, so this example shows no extra tokenizer penalty beyond the UTF-8 byte expansion.

### Q2

Number:750
Why (at most 40 words):The sentence starts beyond the 512-token window and is silently truncated. It cannot help the embedding match the question. Retrieval based only on that sentence is unreliable; coincidental retrieval remains possible, and no explicit error is expected.



### Q3

Number: 74.6%
Why (at most 40 words):Top-p keeps the smallest highest-probability set reaching 95%: Monday, Friday and Sunday. It removes the rest and renormalises. Lower temperature changes relative probabilities before sampling; it does not impose a cumulative-probability cutoff.



### Q4

Number:33.5%
Why (at most 40 words):Exclude multiplication and arithmetic sequences: their answers follow learnable rules. Birthdays and account numbers are arbitrary facts, so weight their singleton rates by question counts. A prompt does not supply missing knowledge or remove this base-model bound.

### Q5

Number:15.3
Why (at most 40 words):he model has 306 tokens per parameter versus Chinchilla's 20, so it is over-trained relative to this compute-optimal criterion. Chinchilla argued that models such as GPT-3 were under-trained: too many parameters for their training-token budget.
