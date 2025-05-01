# Overview of IoT Data Science Processes

- ### Overview of the IoT Data Analysis Process

  - The process begins with the collection and processing of sensor data.
     This includes considering which sensors to use (e.g., motion sensors, current sensors), where the data comes from (phones/wearables for mobile sensing, factories for fixed sensing), and how it is acquired (wireless, wired, hierarchical).
  - Next comes the processing of sensor data, defining the purpose (e.g., activity recognition or fault detection) and the procedure. The typical pipeline includes the phases of **collection → segmentation → feature extraction → classification**.
  - Sensor fusion is also mentioned—i.e., using multiple sensors to achieve better classification.

  ### Mobile Sensing with Smartphones

  - The source introduces the concept of mobile sensing with smartphones, citing a 2010 survey on the topic.
  - The sensors present in a Galaxy S20 are listed: accelerometer, magnetometer (compass), gyroscope, ambient light, proximity, camera, voice, pressure (barometer), NFC, heart rate monitor, and fingerprint scanner.
  - Mobile sensing applications are discussed, including:
    - **Health and well-being** (personal fitness promotion with apps like UbiFit Garden, Move, Google Fit)
    - **Transportation** (traffic conditions with MIT VTrack and Nokia/Berkeley Mobile Millennium, driving behavior with MIT DriveWell)
    - **Social networking** (presence sensing with Dartmouth CenceMe)
    - **Environmental monitoring** (pollution measurement with UCLA PIER and apps like Move and DriveWell)
  - The scales of mobile sensing (individual, group, community) and the sensing paradigms are presented:
    - **Participatory sensing**: active data collection by users (e.g., trash bin monitoring via photos). Advantages include support for complex operations, while challenges relate to data quality depending on participants.
    - **Opportunistic sensing**: automated data collection from sensors (e.g., GPS traces from users' phones). Advantages include less user burden, but challenges include implementation complexity and the phone’s dynamic context (environments).

  ### Architecture of Mobile Sensing

  - The architecture is conceptualized as **Sense → Learn → Inform, Share, Persuasion**
  - The **Sense** phase addresses programmability (sensor management via system APIs, with challenges like fine-grained control and portability), continuous sensing (resource-intensive, requiring energy-efficient algorithms), phone context (dynamic environments affecting data quality, with solutions like admission control and multi-phone collaborative inference), and data/label collection (time-consuming).
  - The **Learn** phase includes sensor data integration, data mining and statistical analysis, and the use of learning algorithms (supervised with labeled data, semi-supervised with partially labeled data, unsupervised with no labels). Examples include activity classification, mobility pattern analysis, and urban noise mapping.
     The issue of **scaling models** for everyday use in dynamic, large-scale environments (millions of people) is addressed, highlighting the need for adaptive models and user integration in the process, potentially using the “wisdom of the crowd.” Challenges include the lack of common ML toolkits for smartphones, large-scale public datasets, and public repositories for data, code, and tool sharing.
  - The **Inform, Share, Persuade** phase deals with sharing (data visualization, community awareness, social networks), personalized services (user preference profiling, recommendations, persuasion), and persuasive technologies (systems that provide targeted feedback to change user behavior in health and environmental awareness domains, using methods like self-reflection, goal setting, and social competition).
     This phase requires **interdisciplinary research** combining behavioral and social psychology with computer science.
  - Privacy issues are highlighted as the most fundamental responsibility of a mobile sensing system. These include personally identifiable data (e.g., voice), **reconstruction attacks** to extract invasive information, and **“data secondhand smoke”** (protecting the privacy of nearby third parties) as well as managing **non-aligned privacy policies** between close individuals.
     The need to understand the **privacy implications** of new mobile and wearable technologies and to develop stronger privacy protection techniques is stressed—such as encryption, privacy-preserving data mining, local data processing, and group sensing apps based on **membership and trust**.

  ### Case Study: Human Activity Recognition via Smartphones

  - A case study is presented on recognizing **high-level human activities** (e.g., giving a lecture, having breakfast, playing soccer) and **low-level ones** (e.g., lying down, standing still, running, walking).
  - The example focuses on recognizing three specific activities: **running**, **standing still**, and **lying down**, using the smartphone’s motion sensors (accelerometer, compass, gyroscope).
  - The activity recognition process is divided into several phases:
     **Sensor data → Data segment → Features → Activity**, with subphases:
     **Data acquisition and preprocessing → Segmentation → Feature extraction → Model construction and classification (inference)**.
  - **Data acquisition and preprocessing** involve collecting a stream of data from sensors (e.g., via Android's sensor manager interface), considering the **sampling rate**.
     The accelerometer is cited as an example, providing acceleration tuples on x, y, and z axes at 5 Hz.
     Android sensing rate configurations are mentioned (SENSOR_DELAY_NORMAL, UI, GAME, FASTEST, or a custom delay in microseconds), noting that actual speed depends on the device and its operational conditions.
  - **Data segmentation** is needed to identify data segments containing activity information (activity detection or spotting). Two approaches are described:
    - **Sliding window**: a window of samples is moved with a fixed overlap (e.g., 50%)
    - **Energy-based**: different activities have different “intensity” or energy (e.g., resting vs. others), and a moving average can be used for automatic segmentation
    - In the example, accelerometer data is collected for 2 seconds (10 readings at 5 Hz) and segmented using a 2-second window with 1-second overlap.
  - **Feature extraction** involves identifying relevant information from the data segments.
     Different types of features are mentioned:
    - **Signal-based**: mean, variance, kurtosis
    - **Body-model-based**: leveraging prior knowledge about human kinematics
    - **Event-based**: when present (e.g., eye movement sequences)
    - **Multilevel**: duration, frequency, co-occurrence, grouped data/labels
    - In the example, the mean of the y-axis signal and the variance of the accelerometer signals are extracted.
  - **Classification** uses the extracted features to determine the current activity via a classifier.
     Many classification algorithms exist, and performance may vary by domain. The result can be a definite decision (e.g., decision tree) or a probability distribution over activities (e.g., Naïve Bayes).
     Learning algorithms can be supervised or unsupervised.
     An example is given using a decision tree to distinguish between "Lying Down", "Standing Still/Running" based on the y-axis mean and variance, also considering orientation and whether the phone is being shaken.
  - The section ends with a summary of the activity recognition process.

  ### Industrial Applications: Machine Condition Monitoring and Fault Diagnosis

  - This section focuses on the use of sensors for machine condition monitoring in industrial settings.
  - Several predictive analysis techniques are described:
     **Vibration analysis** (amplitude/frequency),
     **Oil analysis** (particles, viscosity, acidity),
     **Temperature analysis** (via thermal cameras or temperature sensors), and
     **Ultrasound detection** (to identify faults like corrosion or wear).
  - Sensor node configuration is discussed, comparing **wireless and wired** solutions in terms of reliability and cost. Industrial requirements are highlighted:
     fault tolerance and reliability, preference for long battery life (for wireless), maintainability, integration with existing applications, and security.
  - A deployment experience is presented involving a wireless sensor network in a **semiconductor plant** and in the **North Sea**, detailing the network architecture (server, stargates, sensor nodes, accelerometers) and data transmission reliability.
  - A case study is examined on **AC motor fault monitoring**, using **current transformers (CTs)**, industrial vibration sensors, and MEMS sensors to measure current and acceleration.
     Different motor operating conditions are described (healthy no-load, healthy with resistive load, loose foot, imbalance).
     For feature extraction, **peak-to-peak amplitude** and **signal variance** on a 512-sample window are used.
     The data collection environment is described (motor rotation speed, JN5139 sensor board with IEEE 802.15.4 and ZigBee protocols), as well as training and testing dataset sizes.
     Results are shown comparing performance across different operating conditions, highlighting the best and worst outcomes achieved using **conditional fusion**.

  ### Discussion and Final Summary

  - A comparative discussion is proposed between **personal sensing** and **industrial sensing**, analyzing:
    - **Data acquisition** (sensor types, origin, mode),
    - **Data processing** (purpose, procedure, pipeline, and sensor fusion),
    - and other common and differing issues.
  - The final summary reaffirms key concepts related to:
    - **Mobile sensing with smartphones** (scale, paradigm, Sense-Learn-Inform/Share/Persuade),
    - The **sensor data processing pipeline** (collection, segmentation, feature extraction, model building, evaluation),
    - **Industrial applications** (manual vs. online, pros and cons of wireless networks, use of multiple sensors for fault diagnosis).





# ---------------------------------------------------------------------

# 03 - Context-Aware and Persuasive Computing

## 📍 **1. Context-Aware Computing**

### What is "context"?

- Information that characterizes the **situation of an entity** (person, place, object).
- Models:
  - **Dey (2001)**: Who, What, When, Where → Why?
  - **Schmidt, Beigl, Gellersen (2001)**:
    - Each context has a unique name.
    - A set of relevant features and value ranges are associated with it.

### Examples of context:

- Location, ambient light, motion, temperature, weather, etc.

------

## 🧠 **2. Beyond Simple Context**

### a. Structural Health Monitoring (SHM)

- Sensors are used to detect structural damage in **buildings, bridges, aircraft, turbines**, etc.

### b. Digital Phenotyping / Biomarkers

- Smartphones and wearables collect **biological**, **behavioral**, and **environmental** data.
- Used for health monitoring (e.g., Alzheimer’s detection via mobile data).

------

## 📲 **3. Acquiring Context**

### Sources:

- **Smart environments** (e.g., active badge systems)
- **Mobile sensors** (e.g., accelerometers, cameras, gyroscopes)
- **Sensor fusion**: combining multiple sensors to infer higher-level context

| Context | Cues                                              |
| ------- | ------------------------------------------------- |
| Office  | Artificial light, walking, dry, moderate temp     |
| Jogging | Natural light, running, high pulse, possible rain |

------

## ⚙️ **4. Context-Aware Applications**

### Classification (Schilit et al., 1995):

Two design dimensions: **Manual VS Automatic** and **Information VS Command**.

| Type            | Manual              | Automatic                  |
| --------------- | ------------------- | -------------------------- |
| **Information** | Proximate selection | Contextual reconfiguration |
| **Command**     | Contextual commands | Context-triggered actions  |

### Examples:

- **Proximate Selection**: get information manually, the system makes easier the choice of localized objects. E.g. selecting nearest printer.
- **Contextual Info/Commands**: get information or execute commands manually, basing on user context:
  - Cyberguide (tour guide)
  - GeoNotes (real-world sticky notes)
- **Automatic Reconfiguration**: automatic modification of components/connections of a system basing on the context
  - SenSay phone that adjusts state based on user context
- **Trigger-Action Rules**: simple rules condition-action automatically invoked when a determined condition is met
  - Active Badge: "If I walk past the kitchen, remind me to get coffee"

------

## 🎯 **5. Persuasive Computing**

### Definition (B.J. Fogg):

> "Interactive technology designed to **change attitudes or behaviors**."

### Characteristics:

- Persistent, anonymous, scalable
- Can act where humans cannot (e.g., ubiquitous computing)

### Functional Triad:

| Role             | How it persuades                                             |
| ---------------- | ------------------------------------------------------------ |
| **Tool**         | Makes tasks easier, calculates, guides users                 |
| **Medium**       | Simulates experiences, supports rehearsals, shows consequences |
| **Social Actor** | Offers feedback, models behavior, provides social interaction |

### Examples:

- **Pocket Pikachu**: Pedometer + virtual pet that encourages movement
- **Baby Think It Over**: Infant simulator for teen parenting education

------

## 🤖 **6. Data-Driven In-Situ Interventions**

Pipeline:

1. **Sense** – mobile/wearable sensors collect data
2. **Analyze & Learn** – ML algorithms process patterns
3. **Inform & Act** – personalized, real-time interventions (e.g., “You reached your daily step goal!”)

------

## ❗ **7. Errors in IoT Applications**

### Common Errors:

- **False positives/negatives**: critical depending on context (e.g., fault detection in machines)
- Errors impact **trust** and **usability**

### Solution:

- **Human-in-the-loop**:
  - Machines detect and present info
  - Humans interpret and act on it
  - Encourages **human-AI collaboration**

------

## 📣 **8. Intelligibility + Feedback**

- Users need to understand **why** a system made a decision.
- Types of feedback:
  - **Instance-level**: Was this prediction correct?
  - **Feature-level**: Which features were relevant?

### Effects:

- Poor model accuracy (e.g., 75%) → wrong explanations increase **frustration**, reduce **trust**
- Good model accuracy (e.g., 95%) → explanations improve user **acceptance**

------

## 📌 **9. Final Discussion & Summary**

Students are encouraged to choose a **persuasive + context-aware system/app** and analyze:

- **Context sensing** (how it detects context)
- **Functional triads** (is it a tool, medium, or actor?)
- **Error handling** and **user feedback**

------

## ✅ **Conclusion**

- **Context** is any data that helps define a situation.
- Collected through mobile/wearable sensors and smart environments.
- Used to:
  - Adapt user interfaces and behavior
  - Trigger actions or commands
  - Personalize services
- **Persuasive computing** seeks to **change behavior** through interactive technology.
- Systems need to be **transparent**, **adaptable**, and **collaborative with humans** to be effective and trustworthy.



# ---------------------------------------------------------------------

# 04 - Sensor Datasets

## 📚 **1. Overview of the Lecture**

The lecture focuses on:

- Reviewing sensor datasets
- Exploring several emotion/stress-related datasets:
  - **CrowdSignals.io**
  - **K-EmoCon**
  - **K-EmoPhone**
  - **K-EmoWork**
- Using Google Colab + Pandas + Plotly for data analysis

------

## 🧪 **2. Data Collection Challenges**

- Data collection is one of the **most difficult parts** of sensor-based research.
- **Methods**:
  - **Local Administration (LA)**: Manual recruitment and compensation (e.g., KAIST, Nokia)
  - **App Store-based (AS)**: Apps distributed via app stores (e.g., CenseMe)
  - **Crowdsourced (CS)**: Use platforms like MTurk/Prolific; participants install apps on their own phones

------

## 📱 **3. CrowdSignals.io Dataset**

- **Crowdsourced** mobile data collection platform
- Uses **Experience Sampling Method (ESM)** via lockscreen surveys:
  - Random prompts for participants to report thoughts, feelings, behaviors
- Collects:
  - **Sensor data** from phones
  - **Contextual information** about user activity and state

------

## 💓 **4. K-EmoPhone Dataset**

A large-scale **emotion and stress recognition dataset** collected in-the-wild.

For this dataset, **data collection** was based on a **local administration (LA)** approach, involving direct recruitment of users. Participants used smartphones and wearables to collect data.

Key aspect: Experience Sampling Method (ESM) to gather self-reported data on users' emotional states and stress levels.

------

## 🎤 **5. K-EmoCon Dataset**

Designed for **continuous emotion recognition** during **natural conversations**.

Data collection employed a **retrospective affect annotation protocol**. Participants viewed audio-video recordings of themselves and their partner and annotated their own emotions. This allows collection of both self-reported labels and perceived labels.

------

## 💼 **6. K-EmoWork Dataset**

Emotion, stress, and **emotional workload dataset** for **call center agents**.

Data collection involved **agents listening to recordings** of handled calls and performin retrospective annotations.

### Labeling:

- **Post-call annotation** via **retrospective emotional judgment**
- Mouse cursor tracked at 100–200 ms intervals for continuous feedback

------

## ✅ **Conclusion**

These datasets provide rich multimodal data from **smartphones and wearables** in real-world contexts for:

- Emotion/stress detection
- Human behavior analysis
- Context-aware and affective computing research

They include **self-reported ground truth**, physiological signals, and environmental/behavioral data—enabling advanced analysis and machine learning model development. 

------



# ------------------------------------------------------------------

# 05 - Sensor Data Collection

## 📱 **1. What Is Mobile & Wearable Sensing?**

Mobile and wearable devices collect **digital phenotypes** — personal footprints of:

- **Biological data** (e.g., heart rate)
- **Behavioral data** (e.g., app usage)
- **Environmental data** (e.g., ambient light)

These data are captured **consciously or unconsciously** through smartphones, smartwatches, and IoT devices.

------

## 🎯 **2. Ground Truth Labeling Methods**

### A. Activity Labeling

- **Elicitation**: users follow predefined activity scenarios
- **Natural**: users label activity in real-time (e.g., when it changes)
- **Observation**: third-party labeling in real-time or from videos

### B. Emotion Labeling

- **Elicitation**: emotion induced via videos or tasks (e.g., DEAP dataset)
- **Natural**: self-report using ESM (Experience Sampling Method)
- **Observation**: emotion judged by watching facial expressions, etc.

------

## 🧪 **3. Experience Sampling Method (ESM)**

Also called **Ecological Momentary Assessment (EMA)**

### Key parameters:

- Notification types: **random, interval, event-triggered**
- Expiry time for response (e.g., 3 minutes)
- Inter-notification interval (e.g., 30 min minimum)
- Max daily alerts
- Study duration

### Watch vs. Phone:

- **Micro-interaction** questions on smartwatches increase compliance.
- Shorter and simpler questions = better response rates.

------

## 🔄 **4. Data Fetching Methods**

- **Event-driven**: sensor sends data as soon as available (typical on Android)
- **Polling**: system constantly checks for updates (uses more power)

Buffered sensors use a **producer-consumer model** (FIFO queues) to smooth data collection rates.

------

## 📲 **5. Smartphone Sensor Framework (Android)**

### Key components:

- **SensorManager**: used to access all sensors
- Register sensors via:

```java
sm.registerListener(this, sensor, SensorManager.SENSOR_DELAY_GAME);
```

### Sensor event handling:

    onSensorChanged(SensorEvent event)

- Contains timestamp, accuracy, and sensor values

### Sensor types on Galaxy S20:

- Accelerometer
- Gyroscope
- Magnetometer (compass)
- Light, proximity, pressure (barometer)
- Heart rate, voice, NFC, fingerprint

------

## 🧠 **6. Sensor Types and Their Uses**

| Sensor              | Measures                 | Notes                                 |
| ------------------- | ------------------------ | ------------------------------------- |
| **Accelerometer**   | Acceleration (m/s²)      | Includes gravity                      |
| **Gyroscope**       | Angular velocity (rad/s) | Measures rotation                     |
| **Magnetometer**    | Magnetic field (µT)      | Used for compass orientation          |
| **Light**           | Light intensity (lux)    | Sensitive to ambient light            |
| **Barometer**       | Pressure (mbar)          | Infers altitude indoors               |
| **Proximity**       | Distance (cm)            | Detects near/far object presence      |
| **Activity sensor** | Physical state           | E.g., walking, still, in vehicle      |
| **GPS**             | Location                 | Accuracy ~5m (2m w/ differential GPS) |
| **Microphone**      | Audio/speech             | Used for emotion/behavioral detection |

------

## 💡 **7. Digital Behavior Sensing**

Collected via phone/software logs:

- **App usage**: category, switching behavior
- **Notifications**: handling interactions
- **Typing patterns**: e.g., flight time, hold time, used to detect mental health

------

## ⌚ **8. Wearable Sensors**

### Common Wearables:

- **Empatica E4**: EDA, PPG, temp, movement
- **Polar H10/OH1**: ECG, heart rate, PPG
- **Samsung Watch 3/7**: ECG, SpO₂, motion sensors
- **NeuroSky / Emotiv / OpenBCI**: EEG
- **jins-meme glasses**: EOG (eye movement)

### Sensor modalities:

| Modality | Full Name              | Purpose                   |
| -------- | ---------------------- | ------------------------- |
| **EDA**  | Electrodermal Activity | Emotional arousal         |
| **ECG**  | Electrocardiogram      | Heart electrical activity |
| **PPG**  | Photoplethysmogram     | Blood volume changes      |
| **SpO₂** | Oxygen saturation      | O₂ levels in blood        |
| **EEG**  | Electroencephalogram   | Brain activity            |
| **EOG**  | Electrooculogram       | Eye movements             |

------

## 📊 **9. EDA (Electrodermal Activity)**

- Measures skin conductance
- Increases with emotional arousal
- High density of sweat glands in palms/feet
- Used in lie detectors, stress recognition

------

## ❤️ **10. ECG and PPG**

### ECG:

- Measures heart's electrical impulses
- Captures depolarization events in atria/ventricles

### PPG:

- Measures **blood volume pulse (BVP)**
- Often used in wearables to monitor heart rate
- Easier to use but less precise than ECG

------

## 🌬️ **11. SpO₂ Monitoring**

- Based on red/IR light absorption differences
- Detects **oxygenated vs. deoxygenated hemoglobin**
- Common in smartwatches and medical devices

------

## 👁️ **12. EOG and Eye Tracking**

- Detects eye movement using skin surface potential changes
- Devices like jins-meme or camera-based trackers (e.g., for attention monitoring)

------

## 🔁 **13. Final Review**

### Components of Sensor Data Collection:

- **Labeling**: elicitation, natural reporting (ESM), or third-party observation
- **Fetching**: event-driven vs. polling
- **Smartphone sensors**: Android SDK provides APIs for common sensors
- **Wearable sensors**: provide deeper physiological data
- **Target behaviors**: stress, emotion, activity, engagement, mental health





# ---------------------------------------------------------------------

# 06 - Handling Noise and Missing Values

## 🧭 **1. Lecture Goals**

- Move beyond data collection → now handle **noise** and **missing values**
- Focus on:
  - Outlier detection and removal
  - Imputation of missing values
  - Practical techniques like **Kalman filtering**

------

## ⚠️ **2. What Are Outliers?**

### Types of Outliers:

- **Global outlier**: distant from the overall dataset
- **Contextual outlier**: deviates only within a specific context (e.g., time, location)
- **Collective outlier**: a group of data points deviating together (e.g., attack traffic)

### Causes:

- Sensor faults
- Measurement errors (e.g., a heart rate reading of 400 bpm)
- Subject variability (e.g., real, intense activity)

------

## 📉 **3. Outlier Detection Techniques**

### A. **Distribution-Based Methods**

Assume data follows a **normal distribution**.

- **3×σ Rule**: points beyond 3 standard deviations from the mean
  - ==3×σ from mean==
- **MAD (Median Absolute Deviation)**: more robust than standard deviation
  - ==3×MAD from mean
    MAD = Median(|X$_i$ - median|)==

- **Boxplot Rule**: 
  ==1.5×IQR==
- **Chauvenet’s Criterion**: probabilistic rule to reject unlikely values (e.g., based on sample size). Find a probability band, centered on the mean of a normal distribution that should reasonably contain all N samples of a data set. Remove data outside the band.
  ==Prob = 1 - 1/(2N)==

### B. **Gaussian Mixture Models (GMMs)**

- Model data as a mix of multiple normal distributions (K components)
- Find the best for the parameters by mean of maximizing the likelihood of observing N samples.
- Use **expectation-maximization (EM)** to estimate parameters

### C. **Distance-Based Methods**

- Measure proximity of each point to others using Euclidean distance.
  Points are **close** if they are within distance **d$_{min}$** , **away** if they are placed beyond distance **d$_{min}$**

- **Outlier** = not enough close neighbors (based on thresholds like *d$_{min}$, f$_{min}$*)

  ![image-20250415144638119](/home/luckeez/.config/Typora/typora-user-images/image-20250415144638119.png)

- This approach does not properly take the **local density** into account.

### D. **Local Outlier Factor (LOF)**

- Detects outliers based on **local density**
- Steps:
  1. Find k-nearest neighbors: **k$_{dist_{-}nh}$**   
     Define **k$_{dist}$** as **largest distance** to one of its **k** closest neighbors
  2. Compute reachability distance of **x$_i$** from **x**
     **k$_{reach_{-}dist}$ (x$_i$, x) = max( k$_{dist}$(x) ,  d(x, x$_i$))**
  3. Calculate local reachability density (how close are my neighbors to me?)
  4. Compare density to neighbors → **high LOF = likely outlier**

------

## 🧹 **4. Handling Detected Outliers**

### Options:

- **Remove them**
- **Replace (impute) them** with:
  - Mean / Median / Mode
  - **Interpolated** value (for time-series)
  - **Winsorization** (cap extreme values to percentile thresholds)
    90% winsorization = replace values below and above 5th percentile and 95th percentile (100-90 = 10% both sides), with their nearest value.

------

## 🔧 **5. Missing Value Imputation**

### Common Techniques:

- **Mean/Median/Mode substitution**
- **Interpolation** for time-series (better than mean for smoothness)
- **Similarity-based** (use similar attributes or time periods)

### Example: CrowdSignal heart rate

- Interpolation led to more natural values than using mean

------

## 🔁 **6. Combining Outlier Handling + Imputation**

### **Kalman Filter** (Model-Based Imputation)

- Optimal for **time-series** with known process models
- Requires:
  - State transition model (e.g., motion)
  - Observation model (e.g., GPS, step counter)

#### Steps:

1. **Predict** next state
2. **Correct** prediction using new measurements
3. Adjust based on **Kalman gain** (balancing prediction vs. observed error)

------

## 🔢 **7. Winsorizing Outliers**

- Caps extreme values at thresholds (e.g., 5th/95th percentiles)
- Reduces outlier influence without removing data

------

## 📌 **8. Summary**

### Outlier Detection:

- **ML-based**: hard without labels
- **Distribution-based**: assume normality (σ, MAD, Chauvenet)
- **Distance-based**: global or local density (e.g., LOF)

### Imputation:

- Simple: mean, median, mode, interpolation
- Model-based: Kalman filter
- Robust: Winsorizing



#### **Q: When to use Winsorization and when to Remove outliers?**

##### Winsorization

- When I want to **reduce the influence** of outliers **without losing data**
- When I suspect the **extreme values are valid**, just extreme
- When I'm preparing data for **models sensitive** to outliers (linear regression, k-means, PCA)

##### Remove

- When I'm **sure** outliers are **errors, noise, data entry issues**.
- When extreme values are **not meaningful**
- When the dataset is **large enough**
- When my focus is **robust statistics**



# ---------------------------------------------------------------------

# 07 - Data Quality

## 🧭 **1. Overview & Key Topics**

This lecture covers the importance of **data quality** in IoT-based machine learning and includes:

- Common data quality issues
- **Data-centric AI** (vs. model-centric)
- Dataset development lifecycle
- Data quality metrics & life cycle
- Tools and platforms for ensuring data quality

------

## ⚠️ **2. Data Quality Issues**

### A. **Label Errors**

- Label noise is **pervasive**, even in benchmark datasets (e.g., ImageNet, CIFAR).
- Wrong labels in test data can **destabilize ML benchmarks** and reduce performance.

### B. **Missing Labels**

- Not all sensed data is labeled (especially in continuous sensing).
- The “NULL class” problem arises when sliding windows unintentionally assign invalid labels.

### C. **Common Sensor Data Issues**

- Outliers
- Missing/incomplete data
- **Bias** (e.g., constant offset)
- **Drift**
- **Noise**
- **Constant/stuck values**
- **Uncertainty**

------

## 🔁 **3. Data Cascades**

- **Definition**: Compounding data issues over time → lead to **technical debt**
- Common in **high-stakes AI applications**
- Root cause: "Everyone wants to do the model work, not the data work."

------

## ⚙️ **4. Model-Centric vs. Data-Centric AI**

| Model-Centric AI                | Data-Centric AI                |
| ------------------------------- | ------------------------------ |
| Focuses on tuning models        | Focuses on improving data      |
| Optimizes architecture          | Ensures data quality           |
| Neglects annotation consistency | Iterative model-data co-design |

### Data-Centric AI:

- Improves **fitness and consistency** of data
- Encourages **domain expert collaboration**
- Treats AI as a **sociotechnical system**

------

## 🛠️ **5. Dataset Development Lifecycle**

Inspired by software engineering practices:

1. **Requirements Spec**
    → Who needs the data? Why? What properties?
2. **Design Doc**
    → Are current datasets enough? What are the trade-offs?
3. **Implementation Diary**
    → What challenges occurred during data collection?
4. **Testing Report**
    → Is the dataset usable, valid, and safe?
5. **Maintenance Plan**
    → How to detect staleness, fix errors, and update?

------

## 📊 **6. Quality Metrics (Batini et al., 2009)**

| Metric           | Description                     |
| ---------------- | ------------------------------- |
| **Consistency**  | Format and rules are followed   |
| **Completeness** | No missing data                 |
| **Timeliness**   | Up-to-date data                 |
| **Validity**     | Data reflects real-world events |
| **Uniqueness**   | No duplicates                   |
| **Accuracy**     | Data matches the true value     |

------

## 🤢 **7. Data Smells**

Like “code smells,” **data smells** signal potential issues:

- **Believability**: dummy values, placeholders
- **Understandability**: ambiguous formats
- **Consistency**: format or abbreviation mismatches

------

## 📉 **8. Visualizing and Monitoring Quality**

### Common Practices:

- Plot **data freshness** (e.g., days since last update)
- Visualize **null spikes** (e.g., sudden increase in missing values)
- Detect inconsistencies in real time via dashboards

------

## 🧰 **9. Tools for Data Quality**

### 🔎 **Profiling Tools**:

- **Profiler**: visualizes missing/extreme/inconsistent values
- **AutoProfiler**: adds automation and intelligent suggestions
- **DataPilot**: supports exploratory data profiling

### 🧼 **Cleaning Tools**:

- **Wrangler** (CHI 2011): visual scripting for transformation
- **Tableau Prep**
- **OpenRefine**: open-source data cleanup tool

### 📈 **Tracking Tools**:

- **DataSentry** (CHI 2025):
  - Manages **missing data** during mobile sensor data collection
  - Handles participant dropout, power-offs, sync failures
  - Offers visual diagnosis (per-sensor and per-participant)

------

## 🧪 **10. DataSentry Case Study**

- Multi-year design to support mobile data collection
- Tracks missing data across people/sensors
- Diagnoses:
  - Power-off issues
  - Server/network problems
  - Participant behavior patterns
- Helps researchers communicate better with participants

------

## 🧱 **11. Data Platform Architecture**

### Key Layers:

1. **Data Ingestion**
2. **Storage & Processing**
3. **Transformation & Modeling**
4. **BI & Analytics**
5. **Observability** (monitoring/alerts)
6. **Governance** (documentation, metadata)

------

## 🎮 **12. Real-World Example: Kolibri Games**

### Evolution of their Data Stack:

- **1st Stack**: basic business reporting
- **2nd Stack**: campaign performance, ad spend tracking
- **3rd Stack**: centralization of tools and transparency
- **4th Stack**: advanced analytics and optimization

------

## ✅ **13. Summary**

- **Data quality** is “fitness for use” and is context-dependent.
- **Data-Centric AI** offers a sustainable path to robust systems.
- Quality must be **engineered**, not assumed.
- Use lifecycle documentation + profiling + tracking tools.
- Tools like **DataSentry**, **Profiler**, and **Wrangler** are essential.





# ---------------------------------------------------------------------

# DSP Basics

## **1. Overview**

The document introduces the basics of Digital Signal Processing (DSP), focusing on how analog signals are converted, analyzed, and processed in the digital domain. The core topics include:

- ADC & DAC fundamentals
- Sampling theory and aliasing
- Discrete Fourier Transform (DFT) and its properties
- Practical use of DFT in Python

------

## **2. Analog-to-Digital and Digital-to-Analog Conversion (ADC & DAC)**

- **ADC (Analog-to-Digital Converter)** samples analog signals at regular intervals (every T seconds) and quantizes the result into digital values using `k` bits.
- **DAC (Digital-to-Analog Converter)** reverses the process, turning digital signals back into analog form.
- The document includes a **block diagram** showing a typical DSP system with sampling, quantization, and digital filtering.

------

## **3. Sampling Theory**

### **Nyquist Sampling Rate**

- To avoid information loss, the sampling rate `fs` must be at least **2× the maximum frequency** (`B`) of the input signal.
- For a 10 kHz signal, the minimum `fs` should be 20 kHz.

### **Aliasing**

- Occurs when `fs < 2B`. High-frequency components fold back into the sampled spectrum and distort the signal.
- **Solution**: Apply an **anti-aliasing low-pass filter** before sampling to remove high-frequency noise.

------

## **4. Signal Basics**

- Sinusoidal signals follow:

  $A(t)=A_msin⁡(ωt)=A_msin⁡(2πft)A(t) = A_m \sin(\omega t) = A_m \sin(2\pi f t)A(t)=A_msin(ωt)=A_msin(2πft)$

- Where:

  - `A_m` is amplitude,
  - `f` is frequency,
  - `ω = 2πf` is angular frequency,
  - `T = 1/f` is the period.

------

## **5. DFT and Fourier Analysis**

### Correlation

- Correlation between two signals:

​			$\sum x(i)y(i)$

### **DFT Overview**

- Converts a discrete signal $x(n)$ of length N into its frequency components $X(k)$.
- Each $X(k)$ is computed via correlation with sine and cosine basis functions.

### **Relationship with Other Transforms**

- **FT**: Continuous, aperiodic signals
- **FS**: Continuous, periodic signals
- **DTFT**: Discrete, aperiodic signals
- **DTFS**: Discrete, periodic signals
- **DFT**: Discrete approximation of DTFT, with periodicity assumed

### **DFT Computation**

- Involves using Euler's formula and summing products of the signal with sine/cosine functions.

- Frequency resolution:

  $Δf=fsN\Delta f = \frac{f_s}{N}Δf=Nfs$

------

## **6. DFT Properties**

- **Resolution** improves with:
  - More samples from the signal
  - **Zero-padding** (adding zeros at the end)
- **Symmetry**: For real-valued signals, DFT results exhibit conjugate symmetry.
- **FFT (Fast Fourier Transform)** is a faster algorithm to compute DFT:
   $O(n2)→O(nlog⁡n)O(n^2) \rightarrow O(n \log n)O(n2)→O(nlogn)$

------

## **7. Examples**

### **Example 1**:

DFT of x[n]={1,2,3,4}

### **Example 2**:

Signal: $cos⁡(2πt)$, sampled at 4 Hz
 DFT of x[n]={1,0,−1,0}

- Shows peaks at expected frequency components

### **fftshift**:

- Used to center the zero-frequency component in the DFT output for visualization.

------

## **8. Sampling vs. DFT Resolution**

| Signal Duration | Sampling Rate | #Samples | Δf (Resolution) |
| --------------- | ------------- | -------- | --------------- |
| 1 s             | 20 kHz        | 20,000   | 1 Hz            |
| 2 s             | 20 kHz        | 40,000   | 0.5 Hz          |
| 1 s             | 40 kHz        | 40,000   | 1 Hz            |
| 2 s             | 40 kHz        | 80,000   | 0.5 Hz          |

------

## **9. DFT in Python (using NumPy)**

- `numpy.fft.fft(s)`: forward DFT
- `numpy.fft.ifft(F)`: inverse DFT
- `numpy.fft.fftfreq(n, d)`: frequency bins
- `numpy.fft.fftshift(F)`: center the DC component

------

## **10. Additional Topics**

### **Correlation**

- Measures similarity between two signals.

### **Power and Energy**

- **Energy**: total signal magnitude over time
- **Power**: energy per time unit

### **Decibels (dB)**

- Logarithmic measure of power ratios:
  - Doubling power ≈ +3 dB
  - Halving power ≈ −3 dB





# ---------------------------------------------------------------------

# DSP Filters

## **1. Overview**

The presentation introduces **digital filtering** and its role in **signal analysis and processing**, focusing on:

- Spectral analysis
- Spectral leakage
- FIR and IIR digital filters
- Impulse response & convolution
- Correlation techniques (auto/cross)

------

## **2. Spectral Analysis**

- Converts a time-domain signal into the frequency domain to observe the **frequency spectrum**.
- **White noise** is spread across frequencies (10–70 Hz), while meaningful signals (e.g., 13 Hz) stand out as peaks.
- **Harmonics**: Peaks at multiples of a fundamental frequency, e.g., 13 Hz, 26 Hz, 39 Hz.
- Used in diagnostics, such as **machine condition monitoring** or ECG interpretation.

------

## **3. Spectral Leakage**

- **Occurs when finite-duration windows** are used to analyze signals, especially if they are abruptly cut off.

- Energy from the main frequency “leaks” into adjacent bins, causing misleading artifacts.

- **Windowing** (Hamming, Hanning, Blackman) helps smooth transitions and reduce leakage.

  | Window Length    | Effect on Leakage  |
  | ---------------- | ------------------ |
  | Perfect (2s)     | No leakage         |
  | Truncated (1.8s) | Noticeable leakage |

------

## **4. Digital Filter Basics**

### **What is a Digital Filter?**

- Transforms input sequence `x[n]` into output `y[n]` to **enhance or suppress specific features**, e.g., noise reduction or signal isolation.

### **Impulse Response**

- Defines the output when an impulse is fed into a system:

  $y(n)=x(n)⊗h(n)y(n) = x(n) \otimes h(n)y(n)=x(n)⊗h(n)$

- **Impulse response `h(n)`** characterizes the filter completely.

------

## **5. Convolution in Filtering**

- Filtering = **convolution** between input and filter's impulse response.
- **Acoustic Application**: Convolution reverb simulates how sound reverberates in real spaces.
- Example: Input drumbeat convolved with impulse responses of rooms produces reverb effects.

------

## **6. Frequency Domain Interpretation**

- **Filter’s transfer function H(Ω)**:

  $Y(Ω)=X(Ω)⋅H(Ω)Y(Ω) = X(Ω) \cdot H(Ω)Y(Ω)=X(Ω)⋅H(Ω)$

- In frequency domain, filtering is simple **multiplication**.

- In time domain, it’s **convolution**.

------

## **7. Ideal Low-Pass Filter**

### **Definition**

- Keeps only components below a cutoff frequency `fc`.

### **Problems**

- Ideal filters require infinite impulse responses (`sinc` function).
- Real-world implementation needs **truncation**, which introduces **ripples** and **non-causality**.

### **Solution**

- Truncate and apply **window functions** to mitigate ripples and spectral leakage.
- Trade-off: **More samples** = better accuracy but **slower computation**.

------

## **8. FIR vs. IIR Filters**

| FIR (Finite Impulse Response)   | IIR (Infinite Impulse Response)         |
| ------------------------------- | --------------------------------------- |
| Output depends only on input    | Output depends on input and past output |
| Always stable                   | Can be unstable                         |
| Example: Moving average filter  | Example: Butterworth, Chebyshev filters |
| Easier to design (linear phase) | More efficient (fewer coefficients)     |

------

## **9. Moving Average Filter**

- Simple FIR filter:

  $h[n]=1N for N points h[n] = \frac{1}{N} \text{ for } N \text{ points}, h[n]=N1 for N points$

- Smooths signal but **widens the transition band** as N increases.

------

## **10. IIR Filters**

### **Butterworth Filter**

- **Maximally flat** in the passband (no ripple).
- Higher-order filters approximate ideal low-pass filters better.

### **Chebyshev Filter**

- Allows **controlled ripple** in the passband to achieve **steeper roll-off**.

------

## **11. Filter Design Concepts**

- **Ωp**: Passband frequency
- **Ωs**: Stopband frequency
- **Ωc**: Cutoff frequency (-3 dB point)
- **Transition Band**: Region between passband and stopband
- Design trade-off: narrower transition bands require higher order filters.

------

## **12. Correlation (Auto vs. Cross)**

### **Cross-Correlation**

- Measures similarity between **two signals**, useful for:
  - **Time-delay estimation**
    Compute cross-correlation by multiplying $y[n]$ with many shifted versions of $x[n]$.
    The peak n the record of $r_{xy}[n]$ corresponds to the shift that generates the highest correlation, from which we can deduce the unknown delay.
  - **Signal matching** in noisy environments

### **Autocorrelation**

- Measures similarity of a **signal with itself**, used for:
  - **Period detection**
  - **Heart rate estimation** (e.g., ECG signals)

------

## **13. Applications and Examples**

- **ECG Analysis**:
  - Normal heart rate: 1 Hz peak
  - Flutter: peak at 4 Hz
  - Fibrillation: peak at 5 Hz
- **Machine Monitoring**:
  - Spectral comparison before/after operating periods can indicate wear or faults.

------

## **14. Summary of Key Takeaways**

- Use **spectral analysis** to detect signal features and anomalies.
- Apply **windowing** to minimize spectral leakage.
- Choose filters (FIR or IIR) based on needs: simplicity vs. sharpness.
- Use **convolution** and **correlation** to transform and analyze signals.
- Apply filters in **frequency** or **time domain**, as per convenience.





# -----------------------------------------------------------------

# 10-11 Feature Engineering

## **1. Overview**

The slides focus on **feature engineering** from sensory data to improve performance of machine learning models. Key areas include:

- Numerical and categorical features in the **time domain**
- Frequency domain features via **Fourier analysis**
- **Pattern mining** and **mobility data processing**
- An introduction to **wavelet transforms** for time-frequency analysis

------

## **2. What is Feature Engineering?**

- A **feature** is a measurable property of observed phenomena.
- Good features should be **informative, discriminative**, and **independent**.
- Essential in converting raw sensory data into usable input for machine learning.

------

## **3. Time Domain Features**

### **Numerical Features**

- Computed over sliding windows (`λ` is the window size).
- Examples: **mean, max, min, std**, or more complex metrics (like slope or signal energy).
- **Windowing Types**:
  - **Distinct**: no overlap
  - **Overlapping**: e.g., 50%, 90% overlap
  - More overlap = more data but risk of overfitting

### **Time Domain Co-Lab Tasks**

- Vary window sizes and overlap ratios
- Extract and visualize at least two new features
- Validate timestamp correctness in extracted data

------

## **4. Frequency Domain Features**

### **Fourier Transform**

- Decomposes signal into sinusoidal components using **Fast Fourier Transform (FFT)**.
- Key features:
  - **Peak frequency** (highest amplitude frequency)
  - **Frequency-weighted average**
  - **Power spectrum entropy** (amount of info in the signal, measures signal complexity)

### **Co-Lab Tasks**

- FFT analysis on toy and real data (e.g., CrowdSignals)
- Extract features, apply scaling, and visualize in time domain
- Evaluate how window size affects the frequency spectrum

------

## **5. Categorical Data Features**

- Categorical events like **screen on/off**, **app usage**, or **location types** can yield features such as:
  - **Duration** of a state
  - **Frequency** of changes
  - **Nominal values** (state at time T)

### **Encoding Methods**

To use a "nominal" value as a feature for ML.

- **One-Hot Encoding (Dummy Coding)**: Converts nominal data into binary feature vectors.
  A dummy variable is a variable that can assume either one of two values (1 and 0), 1=existence, 0=not existence.
- If `k` categories exist, dummy coding uses `k–1` binary features to prevent redundancy.

------

## **6. Label Handling and Resampling**

- Labels may be applied to sensor data using time-aligned events.
- Use **resampling + forward-filling** to estimate durations of states (like screen on/off) even across window boundaries.
  1. Create data that consist of activity and start_time
  2. Create data that consist of activity and end_time, and **change the activity in 'unlabeled'**
  3. Concatenate two data row-wise and sort by timestamp
  4. Resample the data by 10 seconds and fill values with **forward-fill**.
- Heatmaps and visualization techniques help assess features across time.

------

## **7. Pattern Mining (Batal et al., 2013)**

- **Temporal patterns** across categorical features:
  - **Succession (`b`)**: one state follows another
  - **Co-occurrence (`c`)**: states occur in the same window
- **Support**: frequency of a pattern's occurrence, used for filtering useful patterns
- Patterns are extended iteratively: start with frequent size-1 patterns and build up

------

## **8. Mobility Data Features**

### **Goal**: Extract meaningful information from GPS data

- Example features:
  - Time spent at “home” or “work”
  - Frequency of location changes

### **Clustering Approaches**

- **DBSCAN** (Density-based):
  - Uses **Haversine distance** for GPS points
  - Parameters: `epsilon`, `minPts`
  - May misclassify roads/intersections as “places” (**false positives**)
- **PoI Clustering** (Point of Interest):
  - Based on **stay points**: areas where the user remains for a defined time and radius
  - More robust for identifying real locations (e.g., offices, homes)

### **Co-Lab Tasks**

- Compare DBSCAN and PoI clustering
- Tune parameters like `epsilon`, `minPts`, `tmax`, and `dmax`
- Visualize GPS clusters on maps

------

## **9. Wavelet Transform (Advanced)**

- **Wavelet transform** captures both **frequency and time** information (unlike FFT, which only captures frequency).
- Based on **scaling and shifting** of a base wavelet function.
- Enables analysis of signals with non-stationary behavior (e.g., sudden changes).

### **Use Case Example**

- Detecting risky mountain trail segments by analyzing walking patterns

------

## **10. Summary of Feature Types**

| Domain          | Feature Types                                      |
| --------------- | -------------------------------------------------- |
| **Time**        | Numerical (mean, std), Categorical, Pattern mining |
| **Frequency**   | FFT-based: peak freq, power, entropy               |
| **Time + Freq** | Wavelet features                                   |
| **Mobility**    | Stay time, location clusters via GPS               |





# ---------------------------------------------------------------------

# 12 - Stat Tests for IoT sensor Data

## **1. Overview**

The presentation covers **how to analyze repeated measurements** commonly found in IoT sensor data. Topics include:

- Why repeated measures matter
- Choosing appropriate **statistical tests**
- When to use **parametric vs. non-parametric tests**
- Advanced modeling approaches: **GEE** and **GLMM**

------

## **2. Repeated Measurements in Sensor Data**

- **Repeated measures** = multiple data points from the same subject or device (e.g., multiple readings from a smartwatch).
- These are **correlated**, violating the independence assumption in many standard statistical tests.
- Context such as **time and location** greatly impacts the interpretation of sensor readings.

------

## **3. Types of Correlation**

- **Within-subject correlation**: Repeated measurements from the same subject.
- **Between-subject correlation**: Correlations across different subjects (e.g., gender, age).

------

## **4. Statistical Tests – Core Concepts**

A **statistical test** is a method to evaluate a hypothesis about a population using sample data.
It determines whether observed differences are likely due to chance or reflect true population differences.

- **Hypotheses**:
  - **Null (H₀)**: No effect or no difference
  - **Alternative (H₁)**: There is a difference
- **p-value**: Probability of the observed outcome if H₀ is true

------

## **5. Choosing the Right Statistical Test**

### **Based on Data Type**

**Parametric data = **follows a specific distribution (mostly normal distribution)

**Paired data = **Repeated measures from a person or machine

| Data Type      | Independent (Unpaired)        | Repeated (Paired)        |
| -------------- | ----------------------------- | ------------------------ |
| Parametric     | t-test / ANOVA                | Paired t-test / RM-ANOVA |
| Non-parametric | Mann-Whitney / Kruskal-Wallis | Wilcoxon / Friedman Test |

- **Normality Check**:
  - **Shapiro-Wilk** (small-medium samples)
  - **Kolmogorov-Smirnov** (large samples)
  - **Q–Q Plot** (visual)

------

## **6. Case Study: AI Counseling Agent**

- Investigated **PHQ-9 depression scores** over three weeks.
- Normality test failed → used **Friedman Test** (non-parametric RM ANOVA).
  Friedman test is a **non-parametric statistical method** for comparing three or more related groups. Used when data violates normality assumptions, is based on **ranking** observations within each subject.
- Result: Significant differences across weeks → conducted **Wilcoxon post-hoc tests**.
  - Week 1–2: slight improvement
  - Week 1–3 & 2–3: significant drops in score

------

## **7. Advanced Case: Interaction of Multiple Factors**

- Example: Compare PHQ-9 scores over time **and** between gender groups.
- Friedman Test can't handle **multi-factor** interactions.

------

## **8. Advanced Models**

### **Generalized Linear Model (GLM)**

- Extends linear regression to handle:
  - Non-normal distributions (Poisson, Gamma, Binomial)
  - Link functions (e.g., logit, identity)
- Assumes independent observations → **not suitable** for repeated measures.

### **Generalized Estimating Equation (GEE)**

- Extension of GLM for **repeated/correlated** data.
- Focus: **population-averaged effects**
- Uses **working correlation structures**, to account for within-subject correlation without specifying random effects:
  - **Independent**: no correlation
  - **Exchangeable**: equal correlation across time points
  - **AR(1)**: time-ordered decay in correlation (e.g., week-to-week symptoms)

#### **GEE Case Study: Counseling Agent**

- Week 2: Small improvement (β = -0.45)
- Week 3: Major improvement (β = -5.45)
- No significant differences between voice/chat groups at week 1

------

### **Generalized Linear Mixed Model (GLMM)**

- Includes both **fixed effects** (e.g., gender, treatment) and **random effects** (e.g., individual differences).
- Models individual variability.
- Suitable for:
  - **Hierarchical data** (e.g., students within schools)
  - **Repeated measures** with individual variation



### GEE vs GLMM

A **random effect **is **non-observed variable** that introduces **variability between groups or units** of observation, that is not directly focused, but still has to be taken into account.

- **GLMM** - Explicitly models the correlation among observations by including **random effects**. It's a **model-based** approach.
  - Includes **fiixed effects**
  - Adds **random effects**
- **GEE** - Focuses on estimating **marginal (population-average)** effects ithout modeling the random variation between subjects. It's an **estimation-based** approach.
  - Only uses **fixed effects**
  - Accounts for correlation by specifying a **working correlation structure** without random effects.



#### **GLMM Case Study: Stress Monitoring**

- Dataset collected via **Experience Sampling Method (ESM)**
- Modelled the effect of:
  - University
  - Gender
  - Screen time (↑ stress)
  - Step count (↓ stress)
- University B and male students showed **higher stress levels**
- No significant gender × university interaction

------

## **9. Summary of Statistical Models**

| Scenario                          | Model              |
| --------------------------------- | ------------------ |
| Parametric, single factor         | RM ANOVA           |
| Non-parametric, single factor     | Friedman Test      |
| Multiple factors (non-parametric) | GEE / ART+RM ANOVA |
| Subject-specific variation        | GLMM               |





# ---------------------------------------------------------------------

# ML Evaluation

## **1. Overview**

The presentation outlines a **complete ML pipeline**, covering everything from **feature selection and model building** to **evaluation and handling imbalanced datasets**. Main topics include:

- Model selection and regularization
- Cross-validation and metrics
- Hyperparameter tuning
- Data scaling, augmentation, and class imbalance strategies

------

## **2. Model Selection and Regularization**

### **Goals**

- Improve **accuracy** and **interpretability**
- Prevent **overfitting**

### **Approaches**

- **Feature selection**: filter out irrelevant features (supervised)
- **Dimension reduction**: PCA, autoencoders (unsupervised).
  Recommended **NOT** to use dimension reduction as feature selection, because can't interpret the meaning of each feature (**less interpretability**).
- **Regularization**: shrink coefficients (L1/L2), embedded in models like Lasso, Ridge, XGBoost.
  To "penalize" too complex models, by reducing **overfitting** and improving **generalization**.
  It helps to obtain more **realistic performances** on new data, as it disallows to **learn noise** and keep models **simpler and more stable.** 



------

## **3. Feature Selection**

### **Methods**

- **Filter methods**: Select features  only based on general data characteristics (e.g., low variance, info gain)
- **Wrapper methods**: Use model performance to evaluate feature subsets.
  Select a subset of features and then iteratively test performance of each model
- **Embedded methods**: Feature selection happens during model training (e.g., Lasso)

### **Examples**

- **Information Gain / Mutual Information**.
  Each feature is assigned a score based on information gained between itself and the class (similar to Gini index)
- **CFS (Correlation-based Feature Selection)**
  Take into account the usefulness of individual features for predicting the class along with the level of inter-correlation among them.



------

## **4. Overfitting and Solutions**

### **Definition**

- Model performs well on training data but poorly on unseen data. It fails to **generalize to unseen data** on test data.

### **Solutions**

- **Early stopping** - stopping the training before it's too much optimized
- Reducing model complexity, to avoid learning from noisy data
- Data augmentation
- Feature selection and regularization

------

## **5. Model Validation Techniques**

### **Standard Methods**

- **Holdout validation**. Simple split of a dataset (80% training, 20% validation)
- **k-fold cross-validation**. Data is divided **randomly** into k parts, each part is held out in turn and the learning scheme trained on the remaining k-1 parts.
- **Leave-one-subject-out (LOSO)**: important in user-independent modeling. If there are **n users**, a model is trained with **n-1** users, and then tested with 1 left out user.
- **Stratified K Fold**. Some classification problems can exhibit a large imbalance in the distribution of the target classes. Relative class frequencies are approximately preserved in each train and validation fold.

### **Common Pitfalls**

- Avoid selecting features **before** splitting the data for CV (leads to optimistic bias).

### **Correct Cross-Validation**

1. Split data into k folds
2. For each fold:
   - Select features that show fairly strong correlations with the class labels, using all of the samples **expect those in fold k**
   - Using just this subset of features, build a multivariate classifier, using all of the samples **except those in fold k**.
   - Use the classifier to predict the class labels for the samples in fold k.

------

## **6. Evaluation Metrics**

### **Binary Classification**

- **Accuracy**: (TP + TN) / All
- **Precision**: TP / (TP + FP)
- **Recall (Sensitivity)**: TP / (TP + FN)
- **F1-score**: Harmonic mean of precision and recall

### **Multiclass**

- **One-vs-All (OvA)** and **One-vs-One (OvO)**
- **Macro, micro, and weighted averages** for metrics
  - **Macro-averaging** - gives equal weight to each class
  - **Weighted-averaging** - based on the number of true samples from each class
  - **Micro-averaging** - gives equal weight to each classification decision


### **Baseline Models**

Learned model should be **better** than dumb models like:	

- **Majority Voting (DumbClassifier)** (e.g., always predict majority class)
- **Random Voting**

### Final Model

Cross-validation is to evaluate a given model.
**Use all the data **to tune the parameters of the final model.

------

## **7. ROC & AUC**

- ROC curves plot **TPR vs. FPR** at various thresholds
- AUC (Area Under Curve): measures overall model performance
- Preferred in **imbalanced** data scenarios

------

## **8. Hyperparameter Tuning**

### **Methods**

- **Grid Search** (exhaustive search)
  Evaluate **all the possible combinations** of hyperparameter values
- **Randomized Search**
  When the hyperparameter search space is large, use randomized search. Try random values among the interval.
- **Bayesian Optimization**
  Keep track of past eval results to form a **probabilistic model** mapping hyperparameters to a probability of a score on the objective function.
- Tools: **Hyperopt, Optuna, Auto-sklearn**

------

## **9. Data and Feature Scaling**

### **Common Techniques**

- Z-score normalization
- Min-max normalization
- Per-person scaling (for personalized signals like heart rate)

### **Why Scale?**

- Crucial for **PCA**, **kNN** (distance-based algorithms), and **neural networks**
- Less important for tree-based methods

------

## **10. Data Augmentation**

### **Techniques for Time Series**

- Rotation, jitter, permutation
- Time warping, magnitude warping
- Cropping and reversing

Used to increase robustness and model generalization.

------

## **11. Handling Imbalanced Data**

### **Problems**

- Classifiers tend to favor the majority class
- Metrics like accuracy can be misleading

### **Solutions**

- **Under-sampling** the majority class
- **Over-sampling** the minority class
- **SMOTE**: synthetic sample generation of minority class
- **Cost-sensitive learning**

### **Evaluation with Imbalance**

- Use **AU-ROC**, **AU-PR curves**, or **balanced accuracy**
- Existing measures are all vulnerable to class imbalance: precision, recall, **f1-score**.
  Avoid just comparing raw f1-scores unless balanced.

------

## **12. Final Model Selection**

- After cross-validation, retrain the final model using **all data** with the best-found parameters.

