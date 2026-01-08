{
  "profileId": "cv_edge_ai",
  "domain": "Edge AI / Embedded AI",
  "headline": "Embedded and AI systems engineer focused on edge AI deployment, on-device inference, and optimized embedded software for real-time intelligent systems.",
  "seniorityTarget": {
    "preferredLevels": ["Intern", "Junior", "Mid"],
    "avoidLevels": ["Senior", "Principal", "Lead Manager"]
  },
  "targetRoles": [
    "Edge AI Engineer",
    "Embedded AI Engineer",
    "Applied AI Engineer (Edge)",
    "TinyML / On-Device AI Engineer"
  ],
  "domainFocus": {
    "coreAreas": [
      "Edge AI deployment",
      "On-device machine learning inference",
      "Embedded software for AI-enabled systems",
      "System optimization for latency and efficiency"
    ],
    "typicalSystems": [
      "Embedded microcontroller-based systems",
      "Smartphones and mobile edge devices",
      "Sensor-driven intelligent systems",
      "AI-enabled robotic and control platforms"
    ],
    "keywordsPriority": {
      "mustHave": [
        "edge AI",
        "on-device inference",
        "embedded software",
        "C/C++",
        "Python",
        "TensorFlow Lite"
      ],
      "strongPlus": [
        "Tiny AI",
        "model optimization",
        "quantized inference",
        "PyTorch",
        "ONNX"
      ],
      "niceToHave": [
        "sensor fusion",
        "real-time systems",
        "Bayesian localization"
      ]
    }
  },
  "techSignature": {
    "languages": ["C", "C++", "Python", "Rust"],
    "microcontrollers": [
      "ATmega328P",
      "ESP32",
      "nRF51822 (ARM Cortex-M0)"
    ],
    "operatingSystems": ["Linux"],
    "frameworks_tools": [
      "TensorFlow Lite",
      "ONNX",
      "PyTorch (learning)",
      "Git",
      "Docker"
    ],
    "protocols": [
      "SPI",
      "I2C",
      "UART"
    ]
  },
  "proofOfWork": {
    "topProjects": [
      {
        "name": "TrackIn: Real-Time Indoor Tracking and Activity Recognition",
        "whatBuilt": "Developed a smartphone-based edge AI system combining Bayesian localization, particle filtering, and an on-device TensorFlow Lite classifier.",
        "hardEvidence": [
          "98% activity classification accuracy",
          "Sub-second inference latency on Android",
          "Multi-sensor fusion using Butterworth filtering"
        ],
        "keywords": [
          "edge AI",
          "TensorFlow Lite",
          "on-device inference",
          "sensor fusion",
          "Tiny AI"
        ]
      },
      {
        "name": "Embedded Quadcopter Control System",
        "whatBuilt": "Implemented a real-time flight control system in Rust with FSM-based safety logic, PID loops, and sensor fusion.",
        "hardEvidence": [
          "Mahony sensor fusion at 200 Hz",
          "Fault-tolerant UART protocol with recovery",
          "Hardware-in-the-loop testing on Cortex-M0"
        ],
        "keywords": [
          "real-time systems",
          "embedded control",
          "sensor fusion",
          "hardware-in-the-loop"
        ]
      }
    ],
    "experienceHighlights": [
      {
        "org": "IMEC",
        "role": "Graduate Research Student",
        "impact": [
          "Designed AeDAM framework for mapping exploration of AI workloads",
          "Built analytical models for energy, latency, and area estimation",
          "Validated models on SENECA neuromorphic architecture"
        ],
        "keywords": [
          "AI workloads",
          "performance modeling",
          "edge accelerator research"
        ]
      }
    ]
  },
  "filters": {
    "hardRejectIf": [
      "Role is purely cloud-based ML with no edge or embedded component",
      "Role is frontend or full-stack web development",
      "Role is data analyst or BI-focused"
    ],
    "softPenalties": [
      "No on-device inference or deployment responsibilities",
      "No embedded or systems-level context"
    ]
  },
  "scoringRubric": {
    "scoreFrom0To100": true,
    "rules": [
      { "if": "job involves edge AI or on-device inference", "delta": 35 },
      { "if": "job mentions TensorFlow Lite or model optimization", "delta": 25 },
      { "if": "job involves embedded software for AI systems", "delta": 20 },
      { "if": "job is cloud-only ML or data science", "delta": -30 },
      { "if": "domain mismatch (non-AI or non-embedded role)", "delta": -40 }
    ],
    "decisionThresholds": {
      "KEEP": 70,
      "MAYBE": 45
    }
  }
}
