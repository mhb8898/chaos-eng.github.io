+++
title = "اصول مهندسی آشوب"
date = 2020-01-28T16:25:57+02:00
draft = true
+++

# PRINCIPLES OF CHAOS ENGINEERING
# اصول مهندسی آشوب
Last Update: 2019 March ([changes](https://github.com/chaos-eng/chaos-eng.github.io/pull/23/files))

*Chaos Engineering is the discipline of experimenting on a system in order to build confidence in the system’s capability to withstand turbulent conditions in production.*
*مهندسی آشوب انضباط بر خواسته از آزمایشاتی است که برای ایجاد اطمینان در سیستم ها با قابلیت پایداری در شرایط پر آشوب به وجود آمده است.*

Advances in large-scale, distributed software systems are changing the game for software engineering.  As an industry, we are quick to adopt practices that increase flexibility of development and velocity of deployment.  An urgent question follows on the heels of these benefits: How much confidence we can have in the complex systems that we put into production?
پیشرفت ها در سیستم های مقیاس پذیر و توزیع شده در حال تغییر بازی در دنیای مهندسی نرم افزار است. به عنوان یک صنعت، ما به دنبال تطبیق با آموزه هایی هستیم که مارا به انعطاف پذیری و سرعت بیشتر در توسعه نرم افزار وفق دهد. یک سوال ضروری به دنبال رسیدن به این دستاورد ها این است که: چه میزان اطمینان به سیستم های پیچیده ای که در محیط واقعی ساخته ایم داریم؟

Even when all of the individual services in a distributed system are functioning properly, the interactions between those services can cause unpredictable outcomes.  Unpredictable outcomes, compounded by rare but disruptive real-world events that affect production environments, make these distributed systems inherently chaotic.
حتی در شرایطی که همه سیستم ها به تنهایی در یک سیستم توزیع شده به خوبی عمل می‌کنند، ارتباط بین آن ها میتواند منجر به نتایج پیشبینی نشده بشود. نتایج غیر قابل پیشبینی، همراه با رویداد های نادر اما مخرب در دنیای واقعی می‌شوند و از این طریق بر محیط توسعه تاثیر می‌گذارند، این چیزی است که سیستم های توزیع شده را ذاتا بی نظم می‌کند.

We need to identify weaknesses before they manifest in system-wide, aberrant behaviors.  Systemic weaknesses could take the form of: improper fallback settings when a service is unavailable; retry storms from improperly tuned timeouts; outages when a downstream dependency receives too much traffic; cascading failures when a single point of failure crashes; etc.  We must address the most significant weaknesses proactively, before they affect our customers in production.  We need a way to manage the chaos inherent in these systems, take advantage of increasing flexibility and velocity, and have confidence in our production deployments despite the complexity that they represent.
ما باید نقاط ضعف را شناسایی کنیم قبل از آنکه به در سطح سیستم آشکار شوند، به وسیله رفتار های ناهنجار. نقاط ضعف سیستماتیک می توانند به شکل: تنظیمات برگشت خطا نامناسب در هنگام فعال نبودن سرویس، قطعی در سیستم به هنگام دریافت ترافیک زیاد در یک وابستگی سرویس، از کار افتادن پشت سر هم چندین سرویس در هنگام خطا در یک نقطه شکست مشترک، و غیره. ما بایدراهی برای مدیریت آشوب ذاتی در این سیستم ها پیدا کنیم، یک قدم برای بهتر شدن انعطاف پذیری، سرعت و داشتن اطمینان در محیط واقعی با وجود تمام پیچیدگی هایی که ارائه می‌کند.

An empirical, systems-based approach addresses the chaos in distributed systems at scale and builds confidence in the ability of those systems to withstand realistic conditions.  We learn about the behavior of a distributed system by observing it during a controlled experiment.  We call this *Chaos Engineering*.
یک آزمایش، راهکاری سیستمی که آشوب را در سیستم های توزیع شده در سطح مقیاس پذیر نشان می‌دهد و در ساختن اطمینان برای ایجاد آن ها در شرایط واقعی نقش بازی می‌کند. ما در رابطه با رفتار سیستم های توزیع شده در یک محیط کنترل شده آزمایشی مشاهداتی را انجام می‌دهیم. ما به این *مهندسی آشوب* می‌گوییم

## CHAOS IN PRACTICE
## آشوب در عمل

To specifically address the uncertainty of distributed systems at scale, Chaos Engineering can be thought of as the facilitation of experiments to uncover systemic weaknesses.  These experiments follow four steps:
برای نشان دادن عدم قطعیت در سیستم های توزیع شده مقیاس پذیر، می‌توان اینگونه فکر کرد که مهندسی آشوب راهی برای آزمایش کردن راحت تر نقاط ضعف سیستم است. این چهار مورد مراحل این آزمایشات هستند:

1. Start by defining ‘steady state’ as some measurable output of a system that indicates normal behavior.
1. در ابتدا با تعریف 'وضعیت پایدار' شروع می‌کنیم با استفاده از تعریف چندین خروجی قابل اندازه گیری که نشان دهد سیستم به صورت طبیعی در حال کار است
2. Hypothesize that this steady state will continue in both the control group and the experimental group.
2. فرض می‌کنیم وضعیت پایدار در گروه آزمایشی و گروه تحت کنترل ادامه می‌یابد
3. Introduce variables that reflect real world events like servers that crash, hard drives that malfunction, network connections that are severed, etc.
3. متغیر هایی می‌سازیم که بودن آن هانشان دهنده اتفاقاتی در دنیای واقعی باشند که باعث ایجاد خرابی هایی مانند از هارد هایی با اشکال در عملکرد، اتصالات شبکه ای که قطع شده اند و غیره است.
4. Try to disprove the hypothesis by looking for a difference in steady state between the control group and the experimental group.
4. سعی می‌کنیم فرضیات مختلف را با مشاهده اختلاف های میان گروه کنترل شده و گروه مورد آزمایش رد کنیم

The harder it is to disrupt the steady state, the more confidence we have in the behavior of the system.  If a weakness is uncovered, we now have a target for improvement before that behavior manifests in the system at large.
هرچه مختل کردن شرایط پایدار سخت تر باشد، اطمینان بیشتری نسبت به پایداری در رفتار سیستم پیدا می‌کنیم. اگر یک نقطه ضعف کشف شود، مابه یک هدف جدید برای بهبود دست پیدا می‌کنیم که می‌توانیم آن را قبل از ورود به محیط وسیع‌تر رفع کنیم.

## ADVANCED PRINCIPLES
## اصول پیشرفته

The following principles describe an ideal application of Chaos Engineering, applied to the processes of experimentation described above.  The degree to which these principles are pursued strongly correlates to the confidence we can have in a distributed system at scale.
اصول زیر نشان دهنده یک کاربرد های ویژه در مهندسی آشوب هستند. با استفاده از مراحل آزمونی که در بالا تعریف کردیم. نمره ای که در این آزمون ها کسب میکنیم به شدت در اطمینان ما از سیستم توزیع شده در مقیاس های بالا موثر است.

### Build a Hypothesis around Steady State Behavior
### ساختن یک فرضیه پیرامون رفتار های وضعیت پایدار


Focus on the measurable output of a system, rather than internal attributes of the system.  Measurements of that output over a short period of time constitute a proxy for the system’s steady state.  The overall system’s throughput, error rates, latency percentiles, etc. could all be metrics of interest representing steady state behavior.  By focusing on systemic behavior patterns during experiments, Chaos verifies that the system does work, rather than trying to validate how it works.
بر روی خروجی قابل اندازه گیری یک سیستم تمرکز کنید، نسبت به ویژگی های داخلی سیستم. 

### Vary Real-world Events

Chaos variables reflect real-world events.  Prioritize events either by potential impact or estimated frequency.  Consider events that correspond to hardware failures like servers dying, software failures like malformed responses, and non-failure events like a spike in traffic or a scaling event.  Any event capable of disrupting steady state is a potential variable in a Chaos experiment.

### Run Experiments in Production

Systems behave differently depending on environment and traffic patterns.  Since the behavior of utilization can change at any time, sampling real traffic is the only way to reliably capture the request path.  To guarantee both authenticity of the way in which the system is exercised and relevance to the current deployed system, Chaos strongly prefers to experiment directly on production traffic.

### Automate Experiments to Run Continuously

Running experiments manually is labor-intensive and ultimately unsustainable.  Automate experiments and run them continuously.  Chaos Engineering builds automation into the system to drive both orchestration and analysis.

### Minimize Blast Radius

Experimenting in production has the potential to cause unnecessary customer pain. While there must be an allowance for some short-term negative impact, it is the responsibility and obligation of the Chaos Engineer to ensure the fallout from experiments are minimized and contained.

Chaos Engineering is a powerful practice that is already changing how software is designed and engineered at some of the largest-scale operations in the world.  Where other practices address velocity and flexibility, Chaos specifically tackles systemic uncertainty in these distributed systems.  The Principles of Chaos provide confidence to innovate quickly at massive scales and give customers the high quality experiences they deserve.

Join the ongoing discussion of the Principles of Chaos and their application in the [Chaos Community](https://groups.google.com/forum/#!forum/chaos-community).
