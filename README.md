# project4
import random

def add_noise(power_consumption):
    noise = random.uniform(-0.1, 0.1) 
    noisy_power = power_consumption + noise
    return noisy_power

def inject_fault(power_consumption):
    fault = random.uniform(-0.5, 0.5)  
    faulty_power = power_consumption + fault
    return faulty_power

def detect_fault(noisy_power_consumption):
    if noisy_power_consumption > 10.05 or noisy_power_consumption < 9.95:
        return True  
    return False
def simulate_fault_detection(num_trials):
    success_count = 0
    base_power_consumption = 10.0  

    for _ in range(num_trials):
        if random.random() < 0.5:  
            power_consumption = inject_fault(base_power_consumption)
        else:
            power_consumption = base_power_consumption

        noisy_power_consumption = add_noise(power_consumption)

        if detect_fault(noisy_power_consumption):
            success_count += 1

    success_rate = success_count / num_trials * 100
    return success_rate

num_trials = 1000
success_rate = simulate_fault_detection(num_trials)
print(f"Success rate of canary tools in detecting fault injection attacks: {success_rate:.2f}%")
