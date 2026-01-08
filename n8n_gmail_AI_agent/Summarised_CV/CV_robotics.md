{
  "profileId": "cv_robotics",
  "domain": "Robotics Software Engineering",
  "headline": "Robotics software engineer with hands-on experience in industrial manipulators, drones, ROS-based systems, and real-time embedded control, focused on reliable hardware–software integration.",
  "seniorityTarget": {
    "preferredLevels": ["Intern", "Junior", "Mid"],
    "avoidLevels": ["Senior", "Principal", "Lead Manager"]
  },
  "targetRoles": [
    "Robotics Software Engineer",
    "Robotics Engineer",
    "Robotics Software Developer",
    "Robotics Systems Engineer"
  ],
  "domainFocus": {
    "coreAreas": [
      "Robot motion control and kinematics",
      "Real-time robotic systems",
      "Hardware–software integration",
      "Robotics system testing and validation"
    ],
    "typicalSystems": [
      "Industrial manipulators (6-axis, 7-axis)",
      "SCARA robots",
      "Mobile and aerial robots",
      "Warehouse automation systems"
    ],
    "keywordsPriority": {
      "mustHave": [
        "robotics",
        "motion control",
        "kinematics",
        "real-time",
        "C++",
        "Python"
      ],
      "strongPlus": [
        "ROS",
        "hardware–software integration",
        "SPI",
        "I2C",
        "UART",
        "embedded systems"
      ],
      "niceToHave": [
        "Gazebo",
        "OpenCV",
        "MQTT",
        "industrial robots",
        "system testing"
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
      "ROS",
      "Git",
      "Docker"
    ],
    "protocols": [
      "SPI",
      "I2C",
      "UART",
      "MQTT"
    ]
  },
  "proofOfWork": {
    "topProjects": [
      {
        "name": "Embedded Quadcopter Control System",
        "whatBuilt": "Implemented a real-time flight control stack in Rust with safety-first FSM, PID loops, and Mahony sensor fusion.",
        "hardEvidence": [
          "Mahony sensor fusion at 200 Hz",
          "Fault-tolerant UART protocol with checksums and recovery",
          "Hardware-in-the-loop testing on Cortex-M0"
        ],
        "keywords": [
          "real-time control",
          "PID",
          "sensor fusion",
          "FSM",
          "embedded robotics"
        ]
      },
      {
        "name": "Vargi Bots – Automated Warehouse Management System",
        "whatBuilt": "Designed a ROS-based warehouse automation system using dual UR5 manipulators, computer vision, and MQTT communication.",
        "hardEvidence": [
          "Robot coordination via modular Python APIs",
          "Simulation and validation in Gazebo",
          "ROS topic introspection and debugging"
        ],
        "keywords": [
          "ROS",
          "industrial robotics",
          "warehouse automation",
          "computer vision"
        ]
      }
    ],
    "experienceHighlights": [
      {
        "org": "UVASKA",
        "role": "Robotics Software Engineer",
        "impact": [
          "Developed software stack for custom 7-axis and 6-axis articulated robots",
          "Implemented kinematics and motion planning algorithms",
          "Integrated hardware interfaces and performed system testing"
        ],
        "keywords": [
          "motion planning",
          "robot kinematics",
          "system integration",
          "industrial manipulators"
        ]
      },
      {
        "org": "Epson",
        "role": "Robotics Software Intern",
        "impact": [
          "Developed Python interface on Raspberry Pi for EPSON SCARA robots",
          "Tested and validated control on physical robot hardware",
          "Assisted in automation system using robot vision module"
        ],
        "keywords": [
          "SCARA robots",
          "robot control",
          "hardware validation"
        ]
      }
    ]
  },
  "filters": {
    "hardRejectIf": [
      "Role is primarily non-robotics software",
      "Role is purely mechanical design with no software responsibility",
      "Role is data analyst or business intelligence focused"
    ],
    "softPenalties": [
      "No robot motion, control, or integration responsibilities",
      "No hands-on robot software development or testing"
    ]
  },
  "scoringRubric": {
    "scoreFrom0To100": true,
    "rules": [
      { "if": "job involves robotics software development or robot control", "delta": 35 },
      { "if": "job mentions ROS or industrial manipulators", "delta": 25 },
      { "if": "job includes motion planning, kinematics, or real-time control", "delta": 20 },
      { "if": "job is primarily simulation-only or theoretical robotics", "delta": -20 },
      { "if": "domain mismatch (non-robotics role)", "delta": -40 }
    ],
    "decisionThresholds": {
      "KEEP": 70,
      "MAYBE": 45
    }
  }
}
