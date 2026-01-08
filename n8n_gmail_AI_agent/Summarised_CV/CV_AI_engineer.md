{
  "profileId": "cv_ai",
  "domain": "AI Software Engineering",
  "headline": "AI software engineer with experience in multimodal models, deep learning systems, performance optimization, and analytical modeling of AI accelerators.",
  "seniorityTarget": {
    "preferredLevels": ["Intern", "Junior", "Mid"],
    "avoidLevels": ["Senior", "Principal", "Lead Manager"]
  },
  "targetRoles": [
    "AI Software Engineer",
    "Machine Learning Engineer",
    "Applied AI Engineer",
    "AI Research Engineer"
  ],
  "domainFocus": {
    "coreAreas": [
      "Deep learning model development",
      "Multimodal AI systems",
      "AI performance modeling and optimization",
      "Data-driven evaluation and benchmarking"
    ],
    "typicalSystems": [
      "Multimodal vision-language models",
      "Neural network training and fine-tuning pipelines",
      "AI workload mapping and accelerator modeling",
      "On-device and edge AI systems"
    ],
    "keywordsPriority": {
      "mustHave": [
        "Python",
        "deep learning",
        "neural networks",
        "machine learning",
        "model training",
        "model evaluation"
      ],
      "strongPlus": [
        "PyTorch",
        "Hugging Face Transformers",
        "multimodal",
        "fine-tuning",
        "ablation studies",
        "performance analysis"
      ],
      "niceToHave": [
        "TensorFlow Lite",
        "CLIP",
        "DeepSpeed",
        "W&B",
        "Bayesian methods"
      ]
    }
  },
  "techSignature": {
    "languages": ["Python", "C", "C++", "Rust"],
    "frameworks_tools": [
      "PyTorch",
      "DeepSpeed",
      "TensorFlow Lite",
      "Hugging Face Transformers",
      "Git"
    ],
    "libraries": [
      "NumPy",
      "Pandas",
      "OpenCV",
      "CLIP",
      "W&B (Weights & Biases)"
    ],
    "operatingSystems": ["Linux"]
  },
  "proofOfWork": {
    "topProjects": [
      {
        "name": "Visual Instruction-Tuned LLaVA for Multimodal Reasoning",
        "whatBuilt": "Reproduced and fine-tuned the LLaVA-1.5 multimodal model integrating CLIP-ViT-L-336px with Vicuna 7B.",
        "hardEvidence": [
          "Ablation study replacing Vicuna 7B with Gemma 2B",
          "Reduced training time by 80% using DeepSpeed ZeRO-3 CPU offloading",
          "Validated inference consistency using CLI benchmarking"
        ],
        "keywords": [
          "multimodal",
          "LLaVA",
          "CLIP",
          "fine-tuning",
          "DeepSpeed",
          "ablation study"
        ]
      },
      {
        "name": "TrackIn: Real-Time Indoor Tracking and Activity Recognition",
        "whatBuilt": "Built a smartphone-based tracking system with Bayesian localization and an on-device TensorFlow Lite classifier.",
        "hardEvidence": [
          "98% activity classification accuracy",
          "Multi-sensor processing using Butterworth filtering",
          "Sub-second inference latency on Android"
        ],
        "keywords": [
          "Bayesian localization",
          "particle filtering",
          "TensorFlow Lite",
          "activity recognition",
          "edge AI"
        ]
      }
    ],
    "experienceHighlights": [
      {
        "org": "IMEC",
        "role": "Graduate Research Student",
        "impact": [
          "Designed AeDAM framework for mapping exploration of AI workloads on event-driven architectures",
          "Built analytical models for energy, latency, and area estimation",
          "Achieved up to 2.5× faster exploration and 52% latency improvement over ZigZag"
        ],
        "keywords": [
          "AI accelerators",
          "mapping exploration",
          "analytical modeling",
          "performance optimization"
        ]
      }
    ]
  },
  "filters": {
    "hardRejectIf": [
      "Role is primarily frontend or full-stack web development",
      "Role is non-technical AI product management",
      "Role is pure data analyst / business intelligence"
    ],
    "softPenalties": [
      "No machine learning or neural network content",
      "No hands-on model development or evaluation"
    ]
  },
  "scoringRubric": {
    "scoreFrom0To100": true,
    "rules": [
      { "if": "job involves deep learning or neural network development", "delta": 35 },
      { "if": "job mentions PyTorch or Hugging Face", "delta": 25 },
      { "if": "job involves model fine-tuning, benchmarking, or evaluation", "delta": 20 },
      { "if": "job is primarily data analytics without ML modeling", "delta": -25 },
      { "if": "domain mismatch (non-AI software role)", "delta": -40 }
    ],
    "decisionThresholds": {
      "KEEP": 70,
      "MAYBE": 45
    }
  }
}
