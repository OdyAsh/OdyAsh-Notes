
Main sources:
* s1: https://www.xda-developers.com/how-to-fast-charge-phone/
	* Less important source
* s2: https://www.xda-developers.com/how-does-fast-charging-work/#how-does-a-smartphone-battery-charge
* s3: https://www.youtube.com/watch?v=9OVtk6G2TnQ


## Understanding Battery Basics

Before diving into fast charging technologies, it's essential to understand basic battery terminology:

- **Voltage (V)**: The electrical potential difference between the battery's terminals, measured in volts. Most smartphone batteries operate at around 3.7-4.2V.

- **Current (A)**: The flow of electric charge, measured in amperes or amps. Higher current means faster charging but also generates more heat.

- **Power (W)**: The rate at which electrical energy is transferred, measured in watts. Power is calculated by multiplying voltage by current (W = V × A). For example, a charger providing 5V at 2A delivers 10W of power.

- **Capacity (mAh)**: The amount of electric charge a battery can store, measured in milliampere-hours. A higher mAh rating means the battery can store more energy and typically last longer between charges.

- **Energy (Wh)**: The total energy stored in a battery, measured in watt-hours. This is calculated by multiplying the voltage by the capacity in ampere-hours (Wh = V × mAh/1000).

* **Buck Converters**: Special circuits used in fast charging technology that convert high voltage to low voltage while simultaneously increasing the current. Unlike standard voltage regulators that limit voltage without changing current (which causes heat buildup), buck converters enable more efficient power conversion with less heat loss. This technology allows manufacturers to use high-voltage chargers (which transmit power more efficiently through cables) while safely converting that power to the correct voltage for smartphone batteries. Modern fast-charging smartphones can use buck converters to handle current values of up to 20A or higher while maintaining the typical 3.7-4.2V that Li-ion batteries require.

## How Lithium-Ion Batteries Work and Charge

Modern smartphones use lithium-ion (Li-ion) batteries because of their high energy density. Unlike simpler battery systems, Li-ion batteries don't charge at a constant rate but go through three distinct stages:

![](Attachments%20-%20Battery%20and%20Charging%20Terminologies%20and%20Technologies/Pasted%20image%2020250414091044.png)

(source: [s2](https://www.xda-developers.com/how-does-fast-charging-work/#how-does-a-smartphone-battery-charge:~:text=three%20separate%20stages))
### 1. Constant Current Phase

When you first connect your phone to a charger, the battery voltage increases rapidly while the current flow remains constant. This is the stage where the fastest charging occurs. During this phase, the battery might charge up to 50-60% of its capacity relatively quickly.

### 2. Saturation Phase

As the battery approaches its peak voltage (typically 4.2V per cell), the charging system needs to be more careful. The voltage increases more slowly while the current remains constant. Li-ion batteries are sensitive to high voltage, so protection systems prevent voltage from exceeding safe values.

### 3. Topping Phase

In the final phase, the voltage reaches its peak value and stops increasing, while the current gradually decreases until the battery is fully charged. This phase takes the longest time proportionally, which is why your phone might charge quickly to 80% but take much longer to reach 100%.

## What is Fast Charging?

Fast charging technology aims to maximize the efficiency of the constant current phase (shown in the image above as the blue horizontal line) to transfer the maximum charge to the battery before reaching the voltage limitations. This is achieved through various methods:

- **Higher Voltage**: Some fast charging technologies increase the voltage (while keeping current moderate) to deliver more power to the device.

- **Higher Current**: Other systems maintain standard voltage but increase the current flow.

- **Intelligent Charging Protocols**: Modern fast charging systems use communication protocols between the device and charger to dynamically adjust voltage and current for optimal charging rates while maintaining safety.

Fast charging is particularly effective during the constant current phase, which is why manufacturers often advertise how quickly their phones can charge from 0% to 50% or 60%, rather than the full 0% to 100%.

## Fast Charging Standards and Technologies

There are three main categories of fast charging standards available today:

### 1. Universal Standards

#### USB Power Delivery (USB-PD)

- Industry-standard protocol that works across multiple devices

- Supports power outputs from 15W up to 240W (in the latest specification)

- Used by many manufacturers including Apple, Google, and Samsung

- PPS (Programmable Power Supply) is an extension that allows for more fine-tuned voltage and current adjustments

#### Qualcomm Quick Charge

- Widely used standard developed by Qualcomm

- Compatible with many Android devices using Qualcomm processors

- Quick Charge 4+ and 5 are backward compatible with USB-PD

- Latest version (QC5) supports up to 100W charging

### 2. Proprietary Standards

These are manufacturer-specific charging technologies that typically offer faster speeds than universal standards but only work with specific devices and chargers:

- **OPPO/OnePlus SuperVOOC**: Up to 240W charging speeds in newer models

- **Xiaomi HyperCharge**: Up to 200W in their fastest implementations

- **Samsung Super Fast Charging**: Up to 45W on select models

- **Apple Fast Charging**: Up to 20-27W depending on the iPhone model

- **Huawei SuperCharge**: Up to 66W on newer models

### 3. Legacy Standards

Older charging standards that are gradually being phased out but still used in some devices:

- **Samsung Adaptive Fast Charging**: Based on Quick Charge 2.0, delivers up to 18W

- **Apple 2.4A Charging**: Older standard limited to about 12W

- **Quick Charge 3.0**: Older but still widely supported Qualcomm standard

## How to Choose the Right Charger for Your Phone

Selecting the right charger involves understanding your device's specific charging capabilities and requirements:

### 1. Check Your Phone's Power Rating

First, identify how much power (in watts) your phone can accept. This information can be found in:

- The phone's manual or specification sheet

- The manufacturer's website

- The label on the original charger that came with the phone

Most smartphones have power ratings between 18W and 65W, though some newer models can support even higher wattages.

### 2. Identify the Charging Protocol Your Phone Supports

Determine which charging standard your phone uses:

- **For iPhones**: Most newer models support USB-PD (Power Delivery)

- **For Android phones with Qualcomm processors**: May support Quick Charge along with USB-PD

- **For phones from brands like OnePlus, Xiaomi, or Huawei**: May have their own proprietary fast charging standards

### 3. Match Charger Specifications to Your Phone's Requirements

Ensure the charger you select:

- Supports the same charging protocol as your device

- Provides sufficient power output (equal to or greater than your phone's requirements)

- Has compatible port types (USB-A, USB-C, Lightning, etc.)

### 4. Consider Multi-Device Charging Needs

If you plan to charge multiple devices with the same charger:

- Check that the charger has sufficient ports for your needs

- Ensure the total power output can adequately distribute power to all connected devices

- Verify that each port supports the necessary charging standards for your devices

## How to Choose the Right Power Bank

When selecting a power bank, consider these factors:

### 1. Capacity

The power bank's capacity (measured in mAh) determines how many times it can charge your device:

- **Smartphone charging**: For most modern smartphones with 3500-5000mAh batteries, a power bank with at least 10,000mAh capacity is recommended for multiple full charges

- **Tablet charging**: For tablets with batteries exceeding 5000mAh, consider power banks with 20,000mAh or more

- **Note**: Due to energy conversion losses, you'll typically get about 60-70% of the rated capacity as usable charge

### 2. Power Output

Check the power bank's output capabilities:

- **Overall output**: The total power the power bank can deliver across all ports

- **Per-port output**: The maximum power each individual port can deliver

- **Fast charging support**: Check which fast charging protocols are supported (USB-PD, Quick Charge, etc.)

### 3. Input Charging Speed

How quickly the power bank itself recharges:

- **Standard input**: Typically 5V/2A (10W), which can take many hours to fully charge larger capacity power banks

- **Fast input charging**: Some power banks support 18W, 30W or even higher input charging, significantly reducing recharge time

### 4. Port Types and Compatibility

Choose a power bank with ports matching your devices:

- **USB-A**: Compatible with most charging cables

- **USB-C**: Newer standard that supports faster charging and is reversible

- **Built-in cables**: Some power banks have integrated cables for specific devices

### 5. Size and Weight

Consider portability based on your needs:

- **Pocket-sized**: 5,000-10,000mAh power banks are typically small enough to fit in a pocket

- **Medium**: 10,000-20,000mAh offer a good balance between capacity and portability

- **High-capacity**: 20,000mAh+ power banks provide more charges but are heavier and larger

## Best Practices for Battery Health

To maximize your battery's lifespan and performance:

### 1. Avoid Extreme Battery Levels

- Try to keep your battery between 20% and 80% for optimal longevity

- Occasional full discharges and charges are acceptable but not necessary

### 2. Manage Heat During Charging

- Remove phone cases that trap heat while charging

- Avoid using processor-intensive apps while fast charging

- Keep your phone in a cool, well-ventilated area during charging

### 3. Use the Right Charging Equipment

- Use high-quality chargers and cables from reputable manufacturers

- Ensure you're using cables that can handle the power requirements of your fast charger

- Match the charging protocol to what your device supports for optimal results

### 4. Be Careful When Using Your Phone While Charging

- **Parasitic Load Explained**: When you use your phone while it's charging, you create what engineers call a "parasitic load." This term refers to a situation where power is being drawn from the battery at the same time it's being charged.

- **How It Works**: During normal charging, electrical current flows from the charger to the battery. When you use your phone while charging, some of the incoming power is diverted to run the phone's components (display, processor, radios, etc.) instead of charging the battery. In some demanding scenarios, your phone might even drain faster than it charges.

- **Impact on Charging Efficiency**: Parasitic loads significantly reduce charging efficiency. Your phone may take much longer to reach a full charge, sometimes 30-50% longer when running intensive applications while charging.

- **Battery Stress Factors**: This simultaneous charging and discharging creates irregular charging patterns that can cause microscopic stress on the battery's internal structure. The battery controller has to constantly adjust its charging algorithm to accommodate the fluctuating power demands.

- **Heat Generation**: The combination of charging heat and processing heat can cause temperature spikes. Modern batteries are particularly sensitive to high temperatures, which accelerate chemical degradation of the cells. Fast charging while gaming or using navigation can push temperatures into ranges that accelerate battery aging.

- **Recommended Approach**: If possible, charge your phone while it's idle or in low-power mode for the most efficient and battery-friendly charging experience. If you must use your phone while charging, try to keep the activities light (occasional messaging rather than gaming or video streaming).

### 5. Overnight Charging Considerations

- Modern phones have protection circuits that prevent overcharging

- However, keeping the battery at 100% for extended periods and at higher temperatures can still cause slight degradation over time

- Consider using scheduled charging features (if available) to complete charging just before you need the device

By following these guidelines and understanding your device's specific charging requirements, you can ensure optimal charging performance while maintaining your battery's health over the long term.