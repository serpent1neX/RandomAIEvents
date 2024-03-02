Adds random AI events such as war declaration, guarantees, insults, etc,... without as much political consequences
Basically turns hoi4 from a war/politics game into a purely war game where you can, of course, WAR, without much consequences like in vanilla such as getting other nations involved.  
Open source, free for modification
v0.0.1a   


```
# Random AI Actions
namespace = random_actions

# Event for AI War Preparation
country_event = {
    id = random_actions.ai_war_preparation
    title = "AI War Preparation"
    desc = "A neighboring country is building up its military forces, preparing for potential aggression."
    picture = GFX_report_event_generic_minor

    is_triggered_only = yes
    trigger = {
        random_country = {
            limit = {
                is_ai = yes
            }
        }
    }

    mean_time_to_happen = {
        days = 360
    }

    option = {
        name = "Monitor the Situation"
        add_political_power = 50
    }

    option = {
        name = "Prepare for Defense"
        add_political_power = -50
        set_country_flag = random_actions.defense_preparedness
    }
}

# Event for Random Declaration of War
country_event = {
    id = random_actions.random_war
    title = "Random War Declaration"
    desc = "A neighboring country has unexpectedly declared war on us!"
    picture = GFX_report_event_generic_minor

    is_triggered_only = yes
    trigger = {
        random_country = {
            limit = {
                is_ai = yes
                has_government = fascism
                has_country_flag = random_actions.defense_preparedness
            }
        }
    }

    mean_time_to_happen = {
        days = 180
    }

    option = {
        name = "Prepare for War"
        add_wargoal = {
            type = annex_everything
            target = ROOT
        }
    }

    option = {
        name = "Seek Diplomacy"
        set_country_flag = random_actions.diplomacy_attempt
    }
}

# Event for Failed Diplomacy Attempt
country_event = {
    id = random_actions.failed_diplomacy
    title = "Failed Diplomacy Attempt"
    desc = "Our diplomatic efforts have failed, leading to rising tensions!"
    picture = GFX_report_event_generic_minor

    is_triggered_only = yes
    trigger = {
        has_country_flag = random_actions.diplomacy_attempt
    }

    mean_time_to_happen = {
        days = 120
    }

    option = {
        name = "Prepare for War"
        add_political_power = -150
        add_wargoal = {
            type = justify_war
            target = ROOT
        }
    }

    option = {
        name = "Attempt Again"
        remove_country_flag = random_actions.diplomacy_attempt
    }
}

# Event for War Outcome
country_event = {
    id = random_actions.war_outcome
    title = "War Outcome"
    desc = "The war has concluded, and the outcome has been determined."
    picture = GFX_report_event_generic_minor

    is_triggered_only = yes
    trigger = {
        has_government = neutrality
        war = {
            is_attacker = yes
            has_concluded = yes
            outcome = won
        }
    }

    mean_time_to_happen = {
        days = 60
    }

    option = {
        name = "Annex the Passive Nation"
        add_wargoal = {
            type = annex_everything
            target = FROM
        }
    }

    option = {
        name = "Retreat and Cede Land"
        add_political_power = -100
        set_country_flag = random_actions.retreat_required
    }
}

# Event for Retreat Outcome
country_event = {
    id = random_actions.retreat_outcome
    title = "Retreat Outcome"
    desc = "The aggressor has retreated, and the passive nation gains territory."
    picture = GFX_report_event_generic_minor

    is_triggered_only = yes
    trigger = {
        has_country_flag = random_actions.retreat_required
    }

    mean_time_to_happen = {
        days = 30
    }

    option = {
        name = "Cede Territory"
        add_wargoal = {
            type = annex_province
            target = ROOT
            province = 123  # Replace with the ID of a neighboring province
        }
    }
}
```
