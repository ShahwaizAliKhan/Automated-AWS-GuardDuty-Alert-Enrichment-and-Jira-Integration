<h1>🛡️ AWS GuardDuty Alert Automation with Tines & Jira</h1>

<p>
This project automates the response to <strong>multiple AWS GuardDuty findings</strong> by using
<strong>Tines</strong> for workflow orchestration and <strong>Jira</strong> for incident tracking.
Findings are streamed from GuardDuty via SNS into Tines, enriched with context, and converted into
Jira tickets with optional remediation actions.
</p>

<p>
The goal is to turn raw GuardDuty alerts into <strong>actionable, enriched, and auditable</strong>
incidents so that security teams can quickly understand what happened, who owns the resource, and
what has already been done to contain the issue.
</p>

<hr>

<h3>🔹 How the automation works</h3>

<p>
GuardDuty monitors AWS resources and generates findings across S3, EC2, IAM, and other services.
These findings are delivered to an SNS topic, which forwards them to a Tines webhook. The Tines
story expands the SNS event, checks that it is a GuardDuty alert, explains it in plain language,
and then fans out into separate branches for different types of threats.
</p>

<ul>
  <li><strong>Alert intake:</strong> SNS sends every GuardDuty finding to a Tines webhook, which expands and validates the event.</li>
  <li><strong>Classification:</strong> The flow distinguishes between S3 exposure, EC2 Command &amp; Control, credential exfiltration, and other supported finding types.</li>
  <li><strong>Jira creation:</strong> A Jira issue is opened with the explanation, severity, affected resources, and recommended actions.</li>
  <li><strong>Optional remediation:</strong> For some findings, Tines can apply S3 bucket block policies, adjust EC2 security groups, or revoke IAM role sessions and log those changes back into Jira.</li>
</ul>

<hr>

<h3>✅ Outcome</h3>

<p>
With this pipeline, GuardDuty findings no longer sit as raw alerts in the console. Instead, they are
centralized in Jira with consistent fields, mapped to owners, and enriched with AWS context. Routine
containment steps are automated, and every action is captured as comments on the corresponding Jira
ticket, providing a complete audit trail from detection to resolution.
</p>

<hr>

<h2>📸 Implementation Screenshots</h2>


<h3>1️⃣ Tines – Full Automation Story</h3>
<p>
End‑to‑end Tines story showing the entire flow from receiving SNS events to creating Jira issues and
branching into S3, EC2 Command &amp; Control, and credential‑related remediation paths.
</p>
<img src="https://github.com/ShahwaizAliKhan/Automated-AWS-GuardDuty-Alert-Enrichment-and-Jira-Integration/blob/main/Project%20Screenshots/full%20story.png" alt="Tines Full GuardDuty Automation Story" width="900">

<hr>

<h3>2️⃣ Tines – Webhook & Event Expansion</h3>
<p>
The entry point of the automation where SNS delivers GuardDuty alerts into Tines, the event is
expanded, and initial checks are performed (including handling the first SNS subscription).
</p>
<img src="https://github.com/ShahwaizAliKhan/Automated-AWS-GuardDuty-Alert-Enrichment-and-Jira-Integration/blob/main/Project%20Screenshots/webhook.png" alt="Tines Receive SNS and Expand Event" width="700">

<hr>

<h3>3️⃣ Tines – AI Explanation of GuardDuty Alert</h3>
<p>
AI action that converts the raw GuardDuty JSON into a human‑readable summary used inside Jira issues
and notifications so analysts can quickly understand the context of the alert.
</p>
<img src="https://github.com/ShahwaizAliKhan/Automated-AWS-GuardDuty-Alert-Enrichment-and-Jira-Integration/blob/main/Project%20Screenshots/AI%20explain.png" alt="Tines AI Explain GuardDuty Alert" width="400">


<hr>


<h3>4️⃣ Tines – Branching & Remediation Logic</h3>
<p>
Branch of the story that checks for S3 public bucket policies, EC2 Command &amp; Control findings,
and credential exfiltration, and then calls HTTP actions to apply S3 block policies, update EC2
security groups, or revoke IAM role sessions while adding comments back to Jira.
</p>
<img src="https://github.com/ShahwaizAliKhan/Automated-AWS-GuardDuty-Alert-Enrichment-and-Jira-Integration/blob/main/Project%20Screenshots/Branching.png" alt="Tines Enrichment and Remediation Branches" width="900">


<hr>


<h3>5️⃣ Tines – Jira Comment Updates</h3>
<p>
Downstream HTTP actions that add detailed comments to existing Jira tickets whenever a remediation
step is executed (for example, after blocking an S3 bucket or revoking an IAM session).
</p>
<img src="https://github.com/ShahwaizAliKhan/Automated-AWS-GuardDuty-Alert-Enrichment-and-Jira-Integration/blob/main/Project%20Screenshots/jira%20comment%20update.png" alt="Tines Adding Jira Comments" width="800">


<hr>


<h3>6️⃣ Jira – GuardDuty Alert Queue</h3>
<p>
Jira project dashboard showing the queue of automatically created “GuardDuty Finding” issues, with
priority, status, and ownership fields used to manage ongoing investigations.
</p>
<img src="https://github.com/ShahwaizAliKhan/Automated-AWS-GuardDuty-Alert-Enrichment-and-Jira-Integration/blob/main/Project%20Screenshots/jira%20queue.png" alt="Jira Project with GuardDuty Findings" width="900">


<hr>


<h3>7️⃣ AWS GuardDuty – Findings View</h3>
<p>
GuardDuty console showing the findings that feed this automation, including sample alerts for EC2,
RDS, Kubernetes, phishing domains, and other threat categories.
</p>
<img src="https://github.com/ShahwaizAliKhan/Automated-AWS-GuardDuty-Alert-Enrichment-and-Jira-Integration/blob/main/Project%20Screenshots/Guardduty%20findings.png" alt="AWS GuardDuty Findings Page" width="900">


<hr>


<h3>8️⃣ AWS IAM – Tines Connector Role</h3>
<p>
IAM role used by Tines to perform actions inside AWS, with permissions such as GuardDuty read access,
S3, EC2, and IAM operations required for enrichment and remediation.
</p>
<img src="https://github.com/ShahwaizAliKhan/Automated-AWS-GuardDuty-Alert-Enrichment-and-Jira-Integration/blob/main/Project%20Screenshots/IAM%20role.png" alt="AWS IAM Role for Tines Connector" width="900">


<hr>


<h3>9️⃣ AWS SNS – GuardDuty Alerts Topic</h3>
<p>
SNS topic configuration that receives GuardDuty findings and forwards them to the Tines webhook
endpoint, providing the event stream that drives the entire workflow.
</p>
<img src="https://github.com/ShahwaizAliKhan/Automated-AWS-GuardDuty-Alert-Enrichment-and-Jira-Integration/blob/main/Project%20Screenshots/SNS%20topic.png" alt="AWS SNS Topic for GuardDuty Alerts" width="900">
<hr>
