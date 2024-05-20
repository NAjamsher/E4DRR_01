---
title: "Home"
date: 2023-10-24
type: landing

design:
  # Default section spacing
  spacing: "6rem"

sections:
  - block: hero
    content:
      title: Advancing Disaster Resilience in Eastern Africa
      text: |
        - 🧱 "E4DRR enhances disaster resilience in Eastern Africa through advanced climate storylines and impact-based forecasting. Our project accelerates targeted assistance for fragile and crisis-affected communities, benefiting over 200 million people by 2026. 
        By fostering data-driven decision-making, we empower stakeholders to effectively manage and mitigate disaster risks, ensuring a more resilient and prepared future for the region.
        Through capacity-building initiatives, we enhance local skills and knowledge, enabling more coordinated and efficient disaster response strategies.
        "  🧱
      #primary_action:
      # text: Get Started
      #url: https://hugoblox.com/templates/
      #icon: rocket-launch
      #secondary_action:
      # text: Read the docs
      #url: https://docs.hugoblox.com
    design:
      spacing:
        padding: [0, 0, 0, 0]
        margin: [0, 0, 0, 0]
      # For full-screen, add `min-h-screen` below
      css_class: "dark"
      background:
        color: "navy"
        image:
          # Add your image background to `assets/media/`.
          filename: tech.jpg
          filters:
            brightness: 0.5
  - block: stats
    content:
      items:
        - statistic: "200M+"
          description: |
            People benefiting  
            from enhanced  
            disaster resilience
        - statistic: "50+"
          description: |
            Countries impacted  
            by advanced  
            climate solutions
        - statistic: "95%"
          description: |
            Accuracy rate  
            in early warning  
            systems
    design:
      # Section background color (CSS class)
      css_class: "bg-gray-100 dark:bg-gray-900"
      # Reduce spacing
      spacing:
        padding: ["1rem", 0, "1rem", 0]
  - block: features
    id: features
    content:
      title: Aims & Impact
      text: Enhancing disaster resilience in Eastern Africa through innovative solutions 🌍
      items:
        - name: Enhanced Risk Awareness
          icon: magnifying-glass
          description: Improved risk knowledge and awareness through advanced climate storylines and impact-based forecasting.
        - name: Timely Assistance
          icon: bolt
          description: Accelerated response times for targeted assistance to vulnerable communities..
        - name: Capacity Development
          icon: sparkles
          description: Building capabilities in disaster management and decision-making through training and workshops.
        - name: Community Engagement
          icon: code-bracket
          description: Engaging stakeholders for co-development and co-production of solutions for disaster resilience.
        - name: Recognized Impact
          icon: star
          description: Recognized impact by global communities and organizations, supporting sustainable development goals.
        - name: Data-Driven Decision Making
          icon: rectangle-group
          description: Empowering decision-makers with data-driven insights for effective disaster management and response strategies.
  - block: cta-image-paragraph
    id: solutions
    content:
      items:
        - title: Enhance Disaster Resilience
          text: Empowering communities with advanced tools and knowledge
          feature_icon: check
          features:
            - "Utilize advanced climate storylines to increase risk awareness among communities, enabling them to better understand and prepare   for potential hazards."
            - "Implement impact-based forecasting methodologies to provide timely and accurate information for disaster response efforts, ensuring    resources are allocated effectively."
            - "Offer capacity development programs to enhance the skills and knowledge of stakeholders involved in disaster management, enabling more efficient and coordinated response strategies."
          # Upload image to `assets/media/` and reference the filename here
          image: 1sol.png

        - title: Collaborative Approach
          text: Engage with stakeholders for sustainable solutions
          feature_icon: bolt
          features:
            - "Facilitate co-development workshops and trainings to involve stakeholders in the design and implementation of disaster resilience solutions, ensuring their needs and perspectives are considered."
            - "Encourage community participation in solution design through engagement activities and feedback mechanisms, fostering a sense of ownership and empowerment among local communities."
            - "Promote stakeholder engagement throughout the project lifecycle to foster partnerships and collaboration, maximizing the impact and sustainability of implemented solutions."
          # Upload image to `assets/media/` and reference the filename here
          image: collab.jpg

    design:
      # Section background color (CSS class)
      css_class: "bg-gray-100 dark:bg-gray-900"
  - block: testimonials
    content:
      title: ""
      text: ""
      items:
        - #name: "Hugo Smith"
          #role: "Marketing Executive at X"
          # Upload image to `assets/media/` and reference the filename here
          #image: "testimonial-1.jpg"
          text: "Incredible tool! The advanced climate storylines and impact-based forecasting have revolutionized our disaster preparedness, making our community safer and more resilient."
    design:
      spacing:
        # Reduce bottom spacing so the testimonial appears vertically centered between sections
        padding: ["6rem", 0, 0, 0]
  - block: cta-card
    content:
      title: Predict and Protect
      text: Harness the power of impact-based forecasting to ensure timely and accurate disaster response, safeguarding vulnerable populations.
      button:
        text: Learn more
        url: /blog
    design:
      card:
        # Card background color (CSS class)
        css_class: "bg-primary-700"
        css_style: ""
---
