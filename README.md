# FLNSim: A Simulator to Evaluate Federated Learning Over Long Range (LoRa) IoT Networks

Copyright (c) 2025 Anshika Singh < a25ec09003@iitbbs.ac.in> and Siddhartha S. Borkotoky <siddhartha.borkotoky@gmail.com> All rights reserved for original contributions and modifications.

This simulator includes and adapts code from the following projects:

1. Flower (flwr) – Federated Learning Framework. Copyright 2020–2025 Flower Labs GmbH (formerly ADAP/University of Oxford). Licensed under the Apache License, Version 2.0. Original source: https://github.com/adap/flower 

2. LoRaSim – Discrete-event LoRa network simulator. Copyright 2016–2017 Thiemo Voigt & Martin Bor. Licensed under the Creative Commons Attribution 4.0 International License (CC BY 4.0). Original source: https://github.com/paafam/LoRaSim  


Note: Portions of this code have been modified from their original implementations. We retain all original notices, copyright statements, and license texts.
This work is licensed under the Creative Commons Attribution 4.0 International License.  To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/.

- ----------------------------------------------------------------------------------------------------

Overview:

The program simulates federated learning sessions (a CNN-based digit classification task on the MNIST dataset) assuming that the server is connected to a LoRa gateway and the clients are LoRa end devices. The simulation outputs are as follows (written to a file output.txt): 

    1. The accuracy of the global model at the end of each round     
    2. The round completion time, defined as the time when all sampled clients finish transmitting their local updates    
    3. The downlink airtime, which is the total time the server spends transmitting in a round    
    4. The cumulative uplink airtime, defined as the total time all sampled clients spend transmitting in a round, aggregated across clients
  
The input parameters are 

    - num_sessions: Number of FL sessions to simulate (final results will be averaged over the sessions)    
    - rounds_per_session: Number of training rounds per session       
    - num_clients: Number of clients
    - network_radius: Network radius in meters (clients will be randomly deployed within a circle of this radius, with the server at the origin)
    - spreading_factor_FL: LoRa spreading factor to be used for transmitting FL updates
    - use_quantization: When set to True, model parameter values will be quantized
    - quantization_bits: Number of quantization bits (supports 1, 2, and 4 bits)
    - use_sparsity: When set to True, model parameters values are sparsified by setting values below a threshold to zero, and if so, what threshold to use
    - sparsity_threshold: Threshold for sparsification
    - apply_zlib: Whether to compress the updates prior to transmission
    - LoRa_Class: The class of LoRaWAN operation to be used (supports class B and C)
    - ping_slot_duration: Ping slot periodicity (only for Class B)
    - Sampling ratio (the fraction of clients chosen for update exchange in each round)
    - FEC_rate: Rate of the FEC applied to the fragments
    - duty_cycle_percentage: Maximum permitted value for transmitter duty cycle (in percentage)
    - interferer_intensity: Number of interferers per sq. meter (assumes a Poisson Point Process)
    - full_simulation: Whether to actually simulate LoRa tranmissions or apply analytical approximations
    - mean_interf_interval: Mean of the time interval (in milliseconds) between two consecutive packets from an interferer
    - interf_payload_range: Range of values for interfering frame payload (an interfering frame carries a payload that is chosen uniformly at random from within this range)             
    - LoRa_channel_code: Defines the channel coding rate for LoRa frames
    - bandwidth: Transmission bandwidth (kHz)
    - Ptx: power of the transmitted signal in dBm
    - path_loss_exponent: Models the exponential decaying of signals
    - num_channels: Number of non-overlapping frequency bands available to LoRa transmitters
