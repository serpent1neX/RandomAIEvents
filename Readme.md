Adds random AI events such as war declaration, guarantees, insults, etc,... without as much political consequences
Basically turns hoi4 from a war/politics game into a purely war game where you can, of course, WAR, without much consequences like in vanilla such as getting other nations involved.  
Open source, free for modification
v0.0.1a   


```
# Random AI Actions
namespace = random_actions

# Event for Random Declaration of War
country_event = {
    id = random_actions.random_war
    title = "Random War Declaration"
    desc = "A neighboring country has declared war unexpectedly!"
    picture = GFX_report_event_generic_minor

    is_triggered_only = yes
    trigger = {
        random_country = {
            limit = {
                is_ai = yes
                has_government = fascism
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
```

    option = {
        name = "Attempt Again"
        remove_country_flag = random_actions.diplomacy_attempt
    }
}
