{
  "profileId": "cv_embedded",
  "domain": "Embedded Systems",
  "headline": "",
  "seniorityTarget": {
    "preferredLevels": ["Intern", "Junior", "Mid"],
    "avoidLevels": ["Senior", "Principal", "Lead Manager"]
  },
  "targetRoles": [
    "Embedded Software Engineer",
    "Firmware Engineer",
    "Robotics/Embedded Engineer"
  ],
  "domainFocus": {
    "coreAreas": [],
    "typicalSystems": [],
    "keywordsPriority": {
      "mustHave": [],
      "strongPlus": [],
      "niceToHave": []
    }
  },
  "techSignature": {
    "languages": [],
    "platforms": [],
    "rtos_os": [],
    "protocols": [],
    "tools": [],
    "testing_debug": []
  },
  "proofOfWork": {
    "topProjects": [
      {
        "name": "",
        "whatBuilt": "",
        "hardEvidence": ["", ""],
        "keywords": ["", ""]
      }
    ],
    "experienceHighlights": [
      {
        "org": "",
        "role": "",
        "impact": ["", ""],
        "keywords": ["", ""]
      }
    ]
  },
  "filters": {
    "hardRejectIf": [
      "Requires X years > 5",
      "Pure web/frontend",
      "Role is mainly sales/marketing"
    ],
    "softPenalties": [
      "No embedded/firmware keywords at all",
      "Only cloud/data keywords"
    ]
  },
  "scoringRubric": {
    "scoreFrom0To100": true,
    "rules": [
      { "if": "matches mustHave keywords strongly", "delta": +35 },
      { "if": "matches strongPlus keywords", "delta": +20 },
      { "if": "seniority mismatch", "delta": -20 },
      { "if": "domain mismatch", "delta": -40 }
    ],
    "decisionThresholds": {
      "KEEP": 70,
      "MAYBE": 45
    }
  }
}
