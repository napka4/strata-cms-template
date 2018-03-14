---
title: 'Fonction Wordpress du jour : Wahoo !'
date: '2018-03-14T18:21:38+01:00'
---
Il y a quelques semaines lors d'un de mes cours de formation sur Node.js, un de mes collègues de promo m'a parlé de ce qu'il faisait avec Wordpress. Et bien sur j'ai ouvert grands les oreilles car c'est mon activité principale !

Et là il m'annonce qu'il modifie et créer des thèmes perso (soit moi aussi je pourrais y arriver si je me penchais vraiment sur la question) avec l'élementor ! En gros il créer des widgets, ou fonctionnalités qu'il intègre à son page builder pour répondre à la demande du client !

Mais TOP !!!! Je dis oui je veux savoir faire ça !

Alors ni une ni deux, on part d'un de mes projets pour un clients perso.

**La base : créer un forum sur Wordpress (again !!), se logguer,poster, et en fonction de si on est loggué ou pas on voit la fonction se logguer ou déco ou s'inscrire !**

Facile? Bah pas avec bbpress, il affiche tout d'un coup et c'est très moche ! Moi je veux un truc qui fasse sérieux quand même ! (You know, I'm a real Developper !)

Donc la solution : créer une classe Auth dans mon thème dans le dossier inc pour créer une condition d'affichage de mon widget.

Je crée donc un dossier "registerTest" dans mon dossier "inc" de mon theme. Puis je crée une classe "Auth". Celle-ci va avoir un : namespace "ForumAlex\RegisterTest"; puis j'utilise Elementor donc une jolie collection de Use :

```
use Elementor\Widget_Base;
```

```
use Elementor\Controls_Manager;
```

```
use Elementor\Group_Control_Background;
```

```
use Elementor\Group_Control_Border;
```

```
use Elementor\Group_Control_Box_Shadow;
```

Ma class extends de Widget_Base :

```
class Auth extends Widget_Base 
```

```

```

```
{
```

```

```

```
    public function get_name()
```

```

```

```
    {
```

```

```

```
        return 'auth';
```

```

```

```
    }
```

```

```

```
    public function get_title()
```

```

```

```
    {
```

```

```

```
        return __('Auth', 'auth');
```

```

```

```
    }
```

```

```

```
    public function get_icon()
```

```

```

```
    {
```

```

```

```
        return 'dashicons-admin-network';
```

```

```

```
    }
```

```

```

```
    protected function _register_controls()
```

```

```

```
    {
```

```

```

```
        $this->start_controls_section(
```

```

```

```
            '_section_style',
```

```

```

```
            [
```

```

```

```
                'label' => __('Element Style', 'elementor'),
```

```

```

```
                'tab' => Controls_Manager::TAB_ADVANCED,
```

```

```

```
            ]
```

```

```

```
        );
```

```

```

```
        $this->add_responsive_control(
```

```

```

```
            '_margin',
```

```

```

```
            [
```

```

```

```
                'label' => __('Margin', 'elementor'),
```

```

```

```
                'type' => Controls_Manager::DIMENSIONS,
```

```

```

```
                'size_units' => ['px', '%'],
```

```

```

```
                'selectors' => [
```

```

```

```
                    '{{WRAPPER}} .elementor-widget-container' => 'margin: {{TOP}}{{UNIT}} {{RIGHT}}{{UNIT}} {{BOTTOM}}{{UNIT}} {{LEFT}}{{UNIT}};',
```

```

```

```
                ],
```

```

```

```
            ]
```

```

```

```
        );
```

```

```

```
        $this->add_responsive_control(
```

```

```

```
            '_padding',
```

```

```

```
            [
```

```

```

```
                'label' => __('Padding', 'elementor'),
```

```

```

```
                'type' => Controls_Manager::DIMENSIONS,
```

```

```

```
                'size_units' => ['px', 'em', '%'],
```

```

```

```
                'selectors' => [
```

```

```

```
                    '{{WRAPPER}} .elementor-widget-container' => 'padding: {{TOP}}{{UNIT}} {{RIGHT}}{{UNIT}} {{BOTTOM}}{{UNIT}} {{LEFT}}{{UNIT}};',
```

```

```

```
                ],
```

```

```

```
            ]
```

```

```

```
        );
```

```

```

```
        $this->add_control(
```

```

```

```
            '_animation',
```

```

```

```
            [
```

```

```

```
                'label' => __('Entrance Animation', 'elementor'),
```

```

```

```
                'type' => Controls_Manager::ANIMATION,
```

```

```

```
                'default' => '',
```

```

```

```
                'label_block' => true,
```

```

```

```
            ]
```

```

```

```
        );
```

```

```

```
        $this->add_control(
```

```

```

```
            'animation_duration',
```

```

```

```
            [
```

```

```

```
                'label' => __('Animation Duration', 'elementor'),
```

```

```

```
                'type' => Controls_Manager::SELECT,
```

```

```

```
                'default' => '',
```

```

```

```
                'options' => [
```

```

```

```
                    'slow' => __('Slow', 'elementor'),
```

```

```

```
                    '' => __('Normal', 'elementor'),
```

```

```

```
                    'fast' => __('Fast', 'elementor'),
```

```

```

```
                ],
```

```

```

```
                'prefix_class' => 'animated-',
```

```

```

```
                'condition' => [
```

```

```

```
                    '_animation!' => '',
```

```

```

```
                ],
```

```

```

```
            ]
```

```

```

```
        );
```

```

```

```
        $this->add_control(
```

```

```

```
            '_css_classes',
```

```

```

```
            [
```

```

```

```
                'label' => __('CSS Classes', 'elementor'),
```

```

```

```
                'type' => Controls_Manager::TEXT,
```

```

```

```
                'default' => '',
```

```

```

```
                'prefix_class' => '',
```

```

```

```
                'label_block' => true,
```

```

```

```
                'title' => __('Add your custom class WITHOUT the dot. e.g: my-class', 'elementor'),
```

```

```

```
            ]
```

```

```

```
        );
```

```

```

```
        $this->end_controls_section();
```

```

```

```
        $this->start_controls_section(
```

```

```

```
            '_section_background',
```

```

```

```
            [
```

```

```

```
                'label' => __('Background & Border', 'elementor'),
```

```

```

```
                'tab' => Controls_Manager::TAB_ADVANCED,
```

```

```

```
            ]
```

```

```

```
        );
```

```

```

```
        $this->add_group_control(
```

```

```

```
            Group_Control_Background::get_type(),
```

```

```

```
            [
```

```

```

```
                'name' => '_background',
```

```

```

```
                'selector' => '{{WRAPPER}} .elementor-widget-container',
```

```

```

```
            ]
```

```

```

```
        );
```

```

```

```
        $this->add_group_control(
```

```

```

```
            Group_Control_Border::get_type(),
```

```

```

```
            [
```

```

```

```
                'name' => '_border',
```

```

```

```
                'selector' => '{{WRAPPER}} .elementor-widget-container',
```

```

```

```
            ]
```

```

```

```
        );
```

```

```

```
        $this->add_control(
```

```

```

```
            '_border_radius',
```

```

```

```
            [
```

```

```

```
                'label' => __('Border Radius', 'elementor'),
```

```

```

```
                'type' => Controls_Manager::DIMENSIONS,
```

```

```

```
                'size_units' => ['px', '%'],
```

```

```

```
                'selectors' => [
```

```

```

```
                    '{{WRAPPER}} .elementor-widget-container' => 'border-radius: {{TOP}}{{UNIT}} {{RIGHT}}{{UNIT}} {{BOTTOM}}{{UNIT}} {{LEFT}}{{UNIT}};',
```

```

```

```
                ],
```

```

```

```
            ]
```

```

```

```
        );
```

```

```

```
        $this->add_group_control(
```

```

```

```
            Group_Control_Box_Shadow::get_type(),
```

```

```

```
            [
```

```

```

```
                'name' => '_box_shadow',
```

```

```

```
                'selector' => '{{WRAPPER}} .elementor-widget-container',
```

```

```

```
            ]
```

```

```

```
        );
```

```

```

```
        $this->end_controls_section();
```

```

```

```
        $this->start_controls_section(
```

```

```

```
            '_section_responsive',
```

```

```

```
            [
```

```

```

```
                'label' => __('Responsive', 'elementor'),
```

```

```

```
                'tab' => Controls_Manager::TAB_ADVANCED,
```

```

```

```
            ]
```

```

```

```
        );
```

```

```

```
        $this->add_control(
```

```

```

```
            'responsive_description',
```

```

```

```
            [
```

```

```

```
                'raw' => __('Attention: The display settings (show/hide for mobile, tablet or desktop) will only take effect once you are on the preview or live page, and not while you\'re in editing mode in Elementor.', 'elementor'),
```

```

```

```
                'type' => Controls_Manager::RAW_HTML,
```

```

```

```
                'classes' => 'elementor-descriptor',
```

```

```

```
            ]
```

```

```

```
        );
```

```

```

```
        $this->add_control(
```

```

```

```
            'hide_desktop',
```

```

```

```
            [
```

```

```

```
                'label' => __('Hide On Desktop', 'elementor'),
```

```

```

```
                'type' => Controls_Manager::SWITCHER,
```

```

```

```
                'default' => '',
```

```

```

```
                'prefix_class' => 'elementor-',
```

```

```

```
                'label_on' => 'Hide',
```

```

```

```
                'label_off' => 'Show',
```

```

```

```
                'return_value' => 'hidden-desktop',
```

```

```

```
            ]
```

```

```

```
        );
```

```

```

```
        $this->add_control(
```

```

```

```
            'hide_tablet',
```

```

```

```
            [
```

```

```

```
                'label' => __('Hide On Tablet', 'elementor'),
```

```

```

```
                'type' => Controls_Manager::SWITCHER,
```

```

```

```
                'default' => '',
```

```

```

```
                'prefix_class' => 'elementor-',
```

```

```

```
                'label_on' => 'Hide',
```

```

```

```
                'label_off' => 'Show',
```

```

```

```
                'return_value' => 'hidden-tablet',
```

```

```

```
            ]
```

```

```

```
        );
```

```

```

```
        $this->add_control(
```

```

```

```
            'hide_mobile',
```

```

```

```
            [
```

```

```

```
                'label' => __('Hide On Mobile', 'elementor'),
```

```

```

```
                'type' => Controls_Manager::SWITCHER,
```

```

```

```
                'default' => '',
```

```

```

```
                'prefix_class' => 'elementor-',
```

```

```

```
                'label_on' => 'Hide',
```

```

```

```
                'label_off' => 'Show',
```

```

```

```
                'return_value' => 'hidden-phone',
```

```

```

```
            ]
```

```

```

```
        );
```

```

```

```
        $this->end_controls_section();
```

```

```

```
    }
```

```

```

```
//ici ma fonction qui gère l'affichage de mon login/register en fonction de si je suis ou non loggué
```

```

```

```
    protected function render()
```

```

```

```
    {
```

```

```

```
        $info = get_currentuserinfo();
```

```

```

```
        ?>
```

```

```

```
        <?php if(!isset($info->user_login)): ?>
```

```

```

```
        <h3>S'enregistrer</h3>
```

```

```

```
            [bbp-register]
```

```

```

```
        <?php endif; ?>
```

```

```

```
        <?php
```

```

```

```
    }
```

```

```

```
}
```

Ensuite mon widget Auth va apparaître dans ma base de widget d'elementor :

![test du widget créer dans elementor](/img/blog/capture d’écran (2)_li.jpg)

Et voilà ce que ça donne : Quand je ne suis pas connecté ou enregistré 

![mon register en fonction de ma connexion](/img/blog/capture d’écran (3).png)

et si je le suis : 

![la fonction s'enregistrer disparaît](/img/blog/capture d’écran (4).png)
