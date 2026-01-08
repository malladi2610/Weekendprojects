{
  "profileId": "cv_embedded",
  "domain": "Embedded Systems",
  "headline": "Embedded software engineer specializing in real-time firmware, microcontroller systems, hardware–software integration, and performance-optimized embedded solutions.",
  "seniorityTarget": {
    "preferredLevels": ["Intern", "Junior", "Mid"],
    "avoidLevels": ["Senior", "Principal", "Lead/Architect"]
  },
  "targetRoles": [
    "Embedded Software Engineer",
    "Firmware Engineer",
    "Real-Time Embedded Engineer",
    "Embedded Systems Developer",
    "IoT/Edge Firmware Engineer"
  ],
  "domainFocus": {
    "coreAreas": [
      "Embedded firmware and real-time systems",
      "Low-level hardware interfacing",
      "Device drivers and BSP integration",
      "Performance, stability, and reliability"
    ],
    "typicalSystems": [
      "MCU-based systems",
      "Sensor/actuator networks",
      "Edge and IoT devices",
      "Robotics/automation controllers"
    ],
    "keywordsPriority": {
      "mustHave": [
        "C", "C++", "embedded firmware",
        "microcontroller", "bare-metal",
        "real-time", "device drivers"
      ],
      "strongPlus": [
        "RTOS", "embedded Linux", "FreeRTOS",
        "UART", "I2C", "SPI", "CAN", "USB"
      ],
      "niceToHave": [
        "Assembly", "ARM Cortex", "debugging tools",
        "hardware-software integration", "optimization"
      ]
    }
  },
  "techSignature": {
    "languages": ["C", "C++", "Rust", "Python", "Assembly (optional)"],
    "platforms": ["ARM Cortex (STM32, nRF)", "AVR", "ESP32", "Raspberry Pi"],
    "rtos_os": ["FreeRTOS", "embedded Linux", "bare-metal"],
    "protocols": ["UART", "SPI", "I2C", "CAN", "USB"],
    "tools": [
      "Git", "GDB", "JTAG/SWD", "Oscilloscope",
      "Logic Analyzer", "Docker/CI/CD"
    ],
    "testing_debug": [
      "unit/integration testing",
      "HIL/embedded test benches",
      "system profiling",
      "performance optimization"
    ]
  },
  "proofOfWork": {
    "topProjects": [
      {
        "name": "Embedded Quadcopter Control System",
        "whatBuilt": "Designed real-time control firmware in Rust + C, implementing PID and sensor fusion loops with strict latency constraints.",
        "hardEvidence": [
          "Rust-based real-time stack with Mahony filter at 200 Hz",
          "Robust UART protocol with CRC, recovery, and watchdog safety"
        ],
        "keywords": ["real-time", "Rust", "firmware", "PID", "sensor fusion"]
      },
      {
        "name": "Cycle-accurate NES Emulator",
        "whatBuilt": "Implemented low-level emulator including CPU, PPU, mappers, interrupts and memory-mapped I/O.",
        "hardEvidence": [
          "Verified across test ROM suite",
          "Detailed instruction timing validation"
        ],
        "keywords": [
          "low-level programming",
          "memory-mapped I/O",
          "system debugging"
        ]
      }
    ],
    "experienceHighlights": [
      {
        "org": "UVASKA",
        "role": "Robotics Software Engineer",
        "impact": [
          "Delivered firmware + control integration for custom robots",
          "Improved hardware interface stability across missions"
        ],
        "keywords": ["C++", "Python", "integration testing", "robotics"]
      },
      {
        "org": "Epson",
        "role": "Robotics Software Intern",
        "impact": [
          "Built Python control interface for SCARA hardware",
          "Validated real hardware control loops in production testbeds"
        ],
        "keywords": ["hardware validation", "system integration"]
      }
    ]
  },
  "filters": {
    "hardRejectIf": [
      "Role is primarily web/frontend or purely cloud/datascience",
      "Role is exclusively hardware design (no firmware)",
      "Position demands >7+ years experience for junior/mid level"
    ],
    "softPenalties": [
      "Few or no embedded-specific keywords",
      "Role focuses mainly on high-level application software with minimal embedded systems context"
    ]
  },
  "scoringRubric": {
    "scoreFrom0To100": true,
    "rules": [
      { "if": "job mentions ≥3 mustHave keywords", "delta": 40 },
      { "if": "job mentions ≥2 strongPlus keywords", "delta": 25 },
      { "if": "role explicitly lists key embedded tasks (real-time, firmware, drivers)", "delta": 20 },
      { "if": "job seniority far above target (e.g., >5y expectation)", "delta": -30 },
      { "if": "domain mismatch (cloud-only, frontend, backend)", "delta": -40 }
    ],
    "decisionThresholds": {
      "KEEP": 75,
      "MAYBE": 50
    }
  }
}
