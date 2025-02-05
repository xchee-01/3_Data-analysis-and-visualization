## Basic Level Questions

#### 1. Create a simple line plot showing patient temperature over 24 hours.

```
times = np.arange(0, 24, 1)  # 24 hours
temperature = [36.8, 36.9, 37.1, 37.0, 36.9, 36.8, 37.0, 37.1, 
               37.2, 37.1, 37.0, 36.9, 36.8, 36.9, 37.0, 37.1,
               37.2, 37.1, 37.0, 36.9, 36.8, 36.9, 37.0, 36.9]
```

> [!TIP]
> Remember to import in Numpy and Matplotlib

  <details>
  <summary>Click to view answer</summary>

  Simple answer 
  
  ```
  plt.plot(times, temperature)
  ```

  More comprehensive answer

  ```
  plt.figure(figsize=(10, 6))
  plt.plot(times, temperature)
  plt.title('Patient Temperature Over 24 Hours')
  plt.xlabel('Time (hours)')
  plt.ylabel('Temperature (°C)')
  plt.grid(True)
  ```

  </details>

#### 2. Create a bar plot showing drug response rates for three different medications.

```
drugs = ['Drug A', 'Drug B', 'Drug C']
response_rates = [65, 78, 45]
```

  <details>
  <summary>Click to view answer</summary>

  Simple answer 
  
  ```
  plt.bar(drugs, response_rates)
  ```

  More comprehensive answer

  ```
  plt.figure(figsize=(8, 6))
  plt.bar(drugs, response_rates)
  plt.title('Drug Response Rates')
  plt.ylabel('Response Rate (%)')
  plt.ylim(0, 100)
  ```

  </details>

#### 3. Create a scatter plot showing the relationship between drug dose and response.

```
doses = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]
responses = [15, 25, 38, 42, 51, 55, 62, 68, 71, 75]
```

  <details>
  <summary>Click to view answer</summary>

  Simple answer 
  
  ```
  plt.scatter(doses, responses)
  ```

  More comprehensive answer

  ```
  plt.figure(figsize=(8, 6))
  plt.scatter(doses, responses)
  plt.title('Drug Dose vs Response')
  plt.xlabel('Dose (mg)')
  plt.ylabel('Response (%)')
  plt.grid(True)
  plt.show()
  ```

  </details>

#### 4. Plot two lines showing treatment outcomes for two different patient groups.

```
weeks = np.arange(0, 13, 4)
group_a = [0, 25, 45, 60]
group_b = [0, 20, 35, 40]
```

  <details>
  <summary>Click to view answer</summary>

  Simple answer 
  
  ```
  plt.plot(weeks, group_a, marker='o', label='Treatment A')
  plt.plot(weeks, group_b, marker='s', label='Treatment B')
  ```

  More comprehensive answer

  ```
  plt.figure(figsize=(10, 6))
  plt.plot(weeks, group_a, marker='o', label='Treatment A')
  plt.plot(weeks, group_b, marker='s', label='Treatment B')
  plt.title('Treatment Response Over Time')
  plt.xlabel('Weeks')
  plt.ylabel('Response (%)')
  plt.legend()
  plt.grid(True)
  plt.show()
  ```

  </details>
