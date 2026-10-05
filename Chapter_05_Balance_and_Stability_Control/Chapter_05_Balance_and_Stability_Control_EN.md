**Volume 21. Quadruped Robot Software**

# Chapter 05. Balance and Stability Control

## 05.01. Stability Criteria Static Dynamic for Quadruped

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

Stability is a fundamental requirement for quadruped locomotion because the robot must continuously prevent its body from falling while supporting itself through discrete foot contacts. Unlike wheeled robots, quadrupeds repeatedly create and remove contact points as they walk. Stability criteria therefore provide mathematical conditions for determining whether the current body state and contact configuration can maintain balance.

Quadruped stability is generally divided into static stability and dynamic stability. Static stability assumes that inertial effects are sufficiently small to be neglected, so balance can be evaluated mainly from gravity and the geometry of supporting contacts. Dynamic stability includes acceleration, momentum, contact forces, and inertial effects, allowing robots to perform faster walking, trotting, running, jumping, and recovery motions.

The support polygon is one of the most important concepts in static stability analysis. It is formed by connecting the ground contact points of the feet that currently support the robot. When all four feet contact flat terrain, the support polygon is approximately quadrilateral. During a crawl gait with one leg swinging, the remaining three supporting feet usually form a triangular support polygon.

For a statically balanced quadruped on level ground, the vertical projection of the center of mass should remain inside the support polygon. If the projected center of mass crosses a polygon boundary, gravity generates a tipping moment about the corresponding support edge. The robot must then modify its posture, establish another contact, or use dynamic motion to prevent falling.

Simply keeping the center-of-mass projection inside the support polygon does not indicate how robust the configuration is. The static stability margin measures the distance between the projected center of mass and the nearest boundary of the support polygon. A larger margin generally indicates greater tolerance to modeling errors, disturbances, terrain irregularities, and small changes in body configuration.

Static stability is especially useful for slow locomotion such as crawling, inspection, manipulation, and traversal of uncertain terrain. A quadruped can deliberately shift its center of mass toward the remaining stance legs before lifting another foot. This approach produces conservative motion but provides predictable balance behavior when precise footholds and reliable ground contact are more important than locomotion speed.

Real terrain complicates static stability because contact points may exist at different heights and orientations. A simple horizontal support polygon can become insufficient on rocks, stairs, slopes, or irregular surfaces. Stability analysis may instead consider a support plane or three-dimensional contact geometry, together with estimated surface normals, friction constraints, and the direction of gravity relative to the robot body.

Dynamic locomotion cannot generally be explained by the center-of-mass projection alone. During a trot, for example, only a diagonal pair of feet may contact the ground, producing a support region that approaches a line. The center of mass does not need to remain statically supported at every instant because controlled acceleration and momentum allow the robot to pass through configurations that would be statically unstable.

The Zero Moment Point, commonly abbreviated as ZMP, provides a classical dynamic stability criterion. It represents the point on the support surface where the resultant tipping moment associated with gravity and inertial forces satisfies the required moment condition. When the ZMP remains within the feasible support region, the contact configuration can theoretically generate the forces needed to resist rotational tipping under the assumed model.

Although ZMP concepts originated largely from legged locomotion studies involving approximately planar support, they remain useful for understanding quadruped balance. Their direct application becomes more difficult when contacts are sparse, noncoplanar, slipping, or rapidly changing. Modern quadruped controllers therefore frequently formulate stability through feasible contact forces rather than relying exclusively on geometric ZMP conditions.

The center of pressure, or CoP, describes the effective location of the resultant ground reaction force within a contact surface. For a finite-sized foot, the CoP must normally remain within the physical contact area if the foot is to maintain surface contact without rotating about an edge. CoP constraints therefore complement whole-body stability conditions by describing the local feasibility of individual foot contacts.

Ground reaction forces are central to dynamic stability. Each stance foot generates forces whose combination must support the robot\'s weight and produce the desired body acceleration and rotational motion. The controller distributes these forces among available contacts while respecting unilateral contact conditions, actuator capability, terrain geometry, and friction limits. Balance therefore becomes a constrained force-allocation problem.

A foot can push against the ground but cannot normally pull the ground toward itself. Consequently, the normal component of contact force must satisfy a unilateral constraint. Tangential force is also limited by friction. These relationships are commonly represented using a friction cone, or a linearized friction pyramid, which defines the range of contact forces that can be generated without slipping.

The centroidal dynamics model provides an efficient representation for analyzing dynamic balance. Instead of modeling every joint independently, it describes the evolution of the robot\'s total linear and angular momentum around its center of mass. Contact forces and their moment arms determine how momentum changes. This formulation connects planned body motion directly with physically feasible stance forces.

Angular momentum becomes particularly important during aggressive locomotion. A quadruped can rotate its trunk, reposition its legs, and redistribute contact forces to regulate body orientation. Stability is therefore not equivalent to keeping the torso perfectly level. Controlled changes in angular momentum may intentionally occur during running, jumping, disturbance rejection, or transitions between different contact configurations.

Another useful concept is the capture point, which describes where support should be established so that the robot can dissipate or redirect its current motion and avoid falling. If a disturbance pushes the robot, merely restoring the center of mass toward the previous support region may be insufficient. The robot may instead need to step in the direction of motion and create a new support configuration.

The capture-point concept illustrates an important distinction between static and dynamic balance. Static stability asks whether the current support geometry can maintain equilibrium, whereas dynamic stability asks whether future motion and contact forces can keep the evolving robot state recoverable. A dynamically stable controller therefore considers velocity and momentum as well as position and contact geometry.

Modern quadrupeds frequently use Model Predictive Control, or MPC, to evaluate stability over a future time horizon. MPC predicts center-of-mass motion, body orientation, contact schedules, and ground reaction forces while enforcing physical constraints. Instead of judging stability from a single instantaneous configuration, the controller searches for a sequence of feasible actions that maintains balance while tracking locomotion objectives.

Whole-body control complements this planning process by converting desired body motion and contact forces into joint-level commands. The controller must satisfy stance constraints while coordinating swing legs, regulating body posture, and respecting joint torque and acceleration limits. Stability criteria consequently operate across several layers, from global motion planning to contact-force optimization and actuator control.

Disturbance rejection provides a practical measure of stability beyond mathematical equilibrium. External pushes, payload movement, foot-placement errors, uneven terrain, and inaccurate state estimation can all move the robot away from its nominal trajectory. A robust quadruped detects these deviations and responds through force redistribution, body adjustment, swing-leg modification, or emergency stepping before balance becomes unrecoverable.

State estimation is therefore inseparable from stability control. The controller requires reliable estimates of body orientation, angular velocity, linear velocity, joint states, foot contacts, and often terrain geometry. IMUs, joint encoders, force sensing, vision, and LiDAR may contribute complementary information. Errors in estimated contact state or body velocity can cause an otherwise valid stability controller to generate inappropriate actions.

Foot-contact transitions are particularly sensitive moments because the feasible support and force regions change abruptly. Before lifting a stance foot, the controller should redistribute load to the remaining contacts. Before relying on a newly placed foot, it should determine whether contact has actually occurred and whether sufficient friction exists. Smooth transitions reduce force discontinuities and improve overall locomotion robustness.

Stability criteria also depend strongly on gait. A crawl gait can maintain a positive static stability margin through much of the cycle, while a trot intentionally accepts configurations with little or no static margin. Bounding and galloping involve even stronger dynamic effects and may include flight phases with no ground contacts. The appropriate criterion must therefore match the locomotion regime rather than imposing one universal geometric rule.

Terrain uncertainty further changes the meaning of stability. A planned foothold may move, deform, or provide less friction than expected. Robust controllers consequently maintain safety margins around friction limits, contact-force bounds, and kinematic constraints. Perception-aware locomotion can additionally select footholds based on estimated slope, roughness, compliance, and traversability instead of treating every reachable location as equally reliable.

Payloads and manipulation tasks can significantly shift the quadruped\'s center of mass and alter its inertia. Carrying equipment, operating a robotic arm, or towing an object changes the forces required to maintain balance. Stability analysis must therefore use the combined robot-payload dynamics whenever these effects are significant, particularly when the payload is large or moves relative to the robot body.

Energy efficiency and stability can sometimes impose competing objectives. Maintaining large static margins may require unnecessary body motion, while aggressive dynamic locomotion may demand high peak forces and rapid actuator responses. Practical controllers balance stability, speed, energy consumption, tracking accuracy, actuator limits, and terrain safety through weighted optimization objectives and carefully selected constraint margins.

A useful stability architecture combines multiple criteria rather than relying on a single metric. Support geometry can provide an intuitive low-speed safety measure, friction constraints can verify contact feasibility, centroidal dynamics can represent momentum evolution, and predictive optimization can assess future recoverability. Together these methods provide a more complete description of quadruped balance across different operating conditions.

Ultimately, quadruped stability is not a fixed property of a posture but a continuously managed relationship among body state, momentum, terrain, contacts, forces, and future actions. Static criteria explain whether gravity can be supported by the current contact geometry, while dynamic criteria determine whether controlled forces and planned contacts can guide the moving system through stable or recoverable trajectories.

Understanding both forms of stability establishes the foundation for advanced quadruped locomotion control. Slow terrain traversal can emphasize center-of-mass projection and static margins, whereas high-performance locomotion requires momentum regulation, friction-aware force optimization, predictive control, and active stepping. A capable quadruped moves continuously between these regimes while preserving feasible contact and recoverable motion.

## 05.02. ZMP and CoP Based Balance Controller [w/Code]

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

Zero Moment Point and Center of Pressure provide closely related concepts for controlling the balance of a quadruped robot through its interaction with the ground. Rather than considering body posture alone, a ZMP- and CoP-based controller evaluates how gravitational, inertial, and contact forces act through the current support region and modifies robot motion to maintain dynamically feasible balance.

The Zero Moment Point, commonly abbreviated as ZMP, is defined on a support surface as the point where the horizontal components of the resultant moment generated by gravity, inertia, and contact reactions satisfy the zero-moment condition. If the calculated ZMP remains inside an admissible support region, the robot can generally generate a contact wrench capable of preventing uncontrolled rotational tipping under the assumed contact model.

The Center of Pressure, or CoP, represents the effective point at which the resultant normal pressure distribution acts on a contact surface. For a rigid flat foot, the CoP should remain inside the physical contact area. If it approaches an edge, the available restoring moment decreases. Once it attempts to move beyond the boundary, the foot may rotate about the edge and the assumed surface-contact condition becomes invalid.

ZMP and CoP are sometimes used interchangeably under simplified conditions, but their meanings are not universally identical. When contacts are planar, rigid, and appropriately modeled, their locations can coincide or become closely related. In general quadruped locomotion, however, multiple contacts, noncoplanar terrain, foot geometry, tangential forces, and external moments require careful distinction between global balance quantities and local pressure behavior.

A balance controller begins by estimating the robot state and identifying the active contact configuration. Body orientation and angular velocity are commonly obtained from an inertial measurement unit, while joint encoders provide leg configuration. Contact sensors, force sensors, motor torque estimates, or observers determine which feet support the body. These estimates establish the support geometry used for subsequent ZMP and CoP calculations.

When several feet are simultaneously in contact with the ground, their contact regions collectively define the feasible support region. For point-foot models this region may be approximated from contact locations, while finite-sized feet provide additional local pressure areas. The controller should normally keep the desired ZMP away from critical boundaries by introducing a stability margin that accommodates uncertainty, disturbances, and imperfect terrain estimation.

A measured or estimated CoP can be calculated from ground reaction forces and contact moments when appropriate sensing is available. For an instrumented foot, pressure or force-torque measurements reveal how load is distributed across the contact surface. For robots without dedicated force sensors, contact forces may instead be estimated from actuator torque, joint dynamics, state observers, or optimization-based whole-body estimation.

The balance-control objective is usually expressed as a desired relationship between body motion and the location of the resultant ground reaction. If the robot body begins moving away from its intended state, the controller shifts the desired ZMP or CoP so that the resulting contact forces create corrective acceleration. Balance regulation therefore depends on actively shaping ground reaction forces rather than merely maintaining a geometrically centered posture.

A simplified inverted-pendulum model provides useful intuition for this relationship. The robot body is approximated as a concentrated mass above the support surface, and the legs regulate the location where the resultant support force acts. Changing the ZMP relative to the center of mass modifies horizontal acceleration. This principle forms the basis of many balance controllers and predictive walking formulations.

The Linear Inverted Pendulum Model, or LIPM, further simplifies the dynamics by assuming approximately constant center-of-mass height and restricted angular-momentum behavior. Under these assumptions, horizontal center-of-mass motion can be directly related to ZMP position. Although a real quadruped violates these assumptions during rough-terrain locomotion, the model remains valuable for planning, analysis, and computationally efficient balance regulation.

A ZMP reference trajectory can be generated from the planned gait and expected contact sequence. During a four-leg stance, the reference can remain well inside the support region. When one leg enters swing, the reference should transition into the region supported by the remaining feet. During trotting, the feasible region becomes narrow because the primary support is provided by a diagonal pair of legs, making dynamic regulation more demanding.

Smooth reference transitions are important because abrupt changes in desired ZMP can require unrealistic changes in ground reaction force. Trajectory generators therefore interpolate the desired support point while considering contact timing, body velocity, and force limits. The transition should begin early enough that load is removed from a departing foot before liftoff and transferred gradually to a newly established contact after touchdown.

CoP control operates at a more direct contact level when the robot has finite foot surfaces. A desired CoP can be assigned within each stance foot according to the required load distribution. The controller then regulates ankle torque, leg force, or whole-body wrench so that the measured pressure center follows the reference. This mechanism can increase resistance to local foot rotation and improve posture regulation.

Many quadrupeds use relatively small or approximately point-like feet and lack actuated ankles. In such systems, local CoP modulation inside a foot is limited compared with humanoid robots. Balance is instead achieved mainly by redistributing forces among multiple legs, changing body acceleration, and adjusting foot placement. The global resultant CoP or equivalent support-force location can nevertheless remain useful for analyzing the combined contact behavior.

Force distribution is commonly formulated as a constrained optimization problem. The desired body wrench is divided among stance legs while satisfying force equilibrium, friction constraints, unilateral contact conditions, and actuator limits. The resulting contact forces determine the effective ZMP or CoP. Optimization allows balance requirements to be combined with posture tracking, energy reduction, smooth force variation, and robustness objectives.

Friction constraints are essential because a mathematically desirable ZMP does not guarantee that the corresponding forces can actually be produced. Excessive horizontal force may cause a stance foot to slip even when the resultant support point lies inside the support region. Controllers therefore enforce friction-cone or friction-pyramid constraints so that planned contact forces remain compatible with estimated terrain friction.

Model Predictive Control provides a powerful framework for ZMP-based balance regulation because it predicts future center-of-mass states and support conditions over a finite horizon. The optimization can select future ZMP references, ground reaction forces, or body accelerations while respecting upcoming contact changes. Predictive control is particularly useful when the feasible support region changes rapidly during locomotion.

Whole-Body Control can execute the balance commands produced by the higher-level planner. Desired center-of-mass acceleration, body orientation, and stance forces are converted into joint torques or joint accelerations while respecting kinematic and dynamic constraints. The ZMP or CoP objective may appear explicitly in this optimization or may emerge indirectly from the optimized distribution of contact forces.

Feedback is necessary because model-based references alone cannot compensate for disturbances and estimation errors. The controller compares measured body states, contact forces, and pressure information with desired values and generates corrective commands. Position, velocity, orientation, and momentum feedback can modify the desired support wrench so that the robot returns toward the planned dynamic state without producing excessively aggressive reactions.

External disturbances illustrate the practical role of ZMP and CoP feedback. When a lateral push accelerates the body, the controller can redistribute ground reaction forces so that the effective support point moves in a direction that produces restoring acceleration. If the required point remains inside the feasible region, balance may be recovered without stepping. Larger disturbances may exceed the available support authority and require foot relocation.

This limitation motivates integration with stepping control. ZMP and CoP regulation are effective only while the required ground reaction can be generated by the current contacts. If the predicted balance point approaches or exceeds the feasible boundary, the controller can modify the next foothold and enlarge or reposition the future support region. Balance control then becomes a coordinated combination of force regulation and contact planning.

Uneven terrain introduces additional complexity because the feet may contact surfaces with different orientations and heights. A single planar ZMP description becomes less accurate when contacts are strongly noncoplanar. The controller may then use projected support planes, contact wrench cones, centroidal dynamics, or direct force optimization while retaining ZMP and CoP quantities as useful diagnostic or reference variables where appropriate.

Contact uncertainty must also be considered. A foot assumed to be supporting the body may partially slip, touch an obstacle at an unexpected location, or fail to establish firm contact. Using such a foot in the support model can produce incorrect ZMP estimates and unsafe force commands. Robust controllers continuously update contact confidence and rapidly redistribute loads when measured forces disagree with the planned contact state.

Sensor filtering is necessary because force, torque, and pressure measurements often contain noise and structural vibration. Excessive filtering, however, introduces delay and can degrade fast balance responses. Practical systems therefore combine appropriately filtered measurements with dynamic observers and state estimators. The balance-control bandwidth should be selected consistently with sensor quality, actuator dynamics, mechanical compliance, and communication latency.

Payload variation changes both the center-of-mass position and the relationship between body acceleration and required contact forces. A ZMP controller designed for an unloaded robot can become biased when a heavy payload is mounted asymmetrically. Accurate mass-property estimation or online adaptation therefore improves balance, especially for quadrupeds carrying manipulators, sensors, cargo, or dynamically moving equipment.

A well-designed ZMP- and CoP-based controller should not attempt to maximize stability margin at every instant. Doing so can unnecessarily restrict locomotion and conflict with desired speed or maneuverability. Instead, the controller maintains sufficient margin while allowing controlled dynamic motion. Safety margins can be adjusted according to gait, terrain confidence, payload, speed, and expected disturbance levels.

The most effective architecture treats ZMP and CoP as components of a broader contact-stability framework rather than complete descriptions of balance. ZMP provides an interpretable relationship between body dynamics and support geometry, while CoP describes how resultant pressure acts through physical contacts. Friction feasibility, momentum dynamics, actuator capability, and future footholds must also be considered for robust quadruped locomotion.

Through this integrated approach, balance control becomes a continuous process of sensing body motion, estimating contacts, predicting feasible support behavior, distributing ground reaction forces, and modifying future steps. ZMP and CoP offer valuable physical quantities linking these operations. When combined with predictive control and whole-body optimization, they provide a practical foundation for stable quadruped locomotion across static and dynamic regimes.

## 05.03. Capture Point and DCM for Quadruped Balance [w/Code]

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

Capture Point and Divergent Component of Motion provide powerful concepts for understanding dynamic balance in quadruped robots. Unlike purely geometric stability criteria, they explicitly consider center-of-mass velocity as well as position. This allows a controller to determine not only whether the robot is currently supported, but also whether its ongoing motion can be stopped, redirected, or recovered through feasible contact actions.

The Capture Point, commonly abbreviated as CP, represents the location at which the robot should establish an effective support point or step so that its center-of-mass motion can be brought toward a balanced state under a simplified dynamic model. A stationary robot may require support near its center of mass, whereas a moving robot generally requires support displaced in the direction of motion to absorb its momentum.

This concept explains why the projection of the center of mass alone is insufficient for dynamic locomotion. A robot can have its center-of-mass projection inside the support region while moving so rapidly that it will soon become unrecoverable. Conversely, the projection may temporarily leave a statically stable region while appropriate momentum and future foot placement still allow successful recovery without falling.

A common mathematical foundation for Capture Point analysis is the Linear Inverted Pendulum Model, or LIPM. The robot is approximated as a point mass moving at approximately constant height above a support surface. Under this assumption, horizontal center-of-mass dynamics contain an unstable component whose evolution depends on center-of-mass position, velocity, gravity, and the effective support point.

For a constant center-of-mass height, the characteristic pendulum frequency is commonly written as omega equal to the square root of gravity divided by center-of-mass height. The Capture Point can then be expressed conceptually as the center-of-mass position plus its horizontal velocity divided by this frequency. Higher velocity therefore moves the required capture location farther in the direction of motion.

The Divergent Component of Motion, or DCM, generalizes this dynamic-state representation. It separates the unstable or divergent component of center-of-mass motion from the convergent component of the inverted-pendulum dynamics. Because the divergent component determines whether the robot moves away from recoverable balance, controlling the DCM provides a direct method for regulating dynamic stability.

Under the standard constant-height LIPM assumptions, the DCM has the same basic expression as the instantaneous Capture Point. The terminology emphasizes a different interpretation: Capture Point focuses on where support should be established to stop the motion, while DCM emphasizes the continuously evolving unstable state that must be controlled through contact forces, support-point modulation, or future stepping.

DCM dynamics are particularly useful because their future evolution can be predicted from the relationship between the DCM and the effective support point. If the support point remains fixed while the DCM is displaced from it, the divergent state tends to move away exponentially. The controller must therefore manipulate support forces or change contacts before the DCM leaves the region from which recovery is physically possible.

For a quadruped in a multi-leg stance, the effective support point can be regulated by redistributing ground reaction forces among the stance feet. If the required DCM correction is relatively small, the controller may restore balance without moving any foot. It changes the resultant support force so that center-of-mass acceleration redirects the divergent motion toward the desired trajectory.

The available force redistribution is limited by contact geometry, friction, and actuator capability. A desired support point cannot be arbitrarily placed outside the region achievable by the active contacts. If DCM regulation requires a support action beyond these limits, the robot must modify its contact configuration. This creates a natural connection between continuous balance control and discrete footstep planning.

Stepping extends the recoverable region by creating a new support location. When a disturbance pushes the robot forward, for example, the DCM shifts forward because both center-of-mass position and velocity contribute to it. The controller can place a swing foot farther forward so that the future support region captures the evolving DCM and produces the forces needed to reduce forward motion.

Quadruped robots provide more contact choices than bipeds because any combination of available legs may contribute to recovery. Depending on the gait phase, the controller can alter the next foothold, accelerate an ongoing swing, delay liftoff, prolong stance, or change the planned contact sequence. DCM-based reasoning helps determine which modification most effectively restores a recoverable dynamic state.

The desired DCM trajectory can be constructed from a planned sequence of support conditions. Rather than commanding abrupt changes at contact transitions, the planner generates a continuous evolution consistent with future footholds and gait timing. The desired center-of-mass trajectory can subsequently be derived or regulated so that its motion remains compatible with the DCM reference and the available support actions.

Footstep location and contact timing are strongly coupled in DCM control. Moving a foot farther in the disturbance direction can increase recovery capability, but the benefit may arrive too late if the swing duration is long. Reducing swing time can provide earlier support but may demand higher joint velocity and acceleration. Practical recovery planning therefore optimizes both spatial and temporal contact decisions.

A useful extension is the concept of capturability, which describes whether the robot can reach a stable or bounded state using a feasible number of future contacts. One-step capturability asks whether a single new foothold can recover balance, while multi-step capturability considers sequences of steps. This provides a richer stability measure than simply checking whether the current DCM lies inside an instantaneous support region.

Capture regions represent sets of feasible footholds capable of recovering a given dynamic state. Their size and shape depend on leg reachability, center-of-mass velocity, contact timing, terrain geometry, friction, and actuator limits. For quadrupeds, capture-region reasoning can be combined with kinematic workspace constraints so that a theoretically stabilizing step is not selected if the leg cannot physically reach it.

Model Predictive Control can incorporate DCM behavior over a finite horizon. The optimizer predicts future body states, contact phases, and support actions while selecting ground reaction forces or footholds that keep the divergent motion bounded. This predictive formulation is valuable during trotting or rapid gait transitions because the current contact set may offer limited authority while future contacts provide additional recovery capability.

DCM control can also be integrated with centroidal dynamics. The simplified inverted-pendulum formulation offers computational efficiency and intuitive balance variables, while centroidal models represent linear and angular momentum more accurately. A hierarchical architecture may therefore use DCM for high-level recovery planning and a centroidal or whole-body optimizer for dynamically feasible force and torque realization.

Angular momentum introduces an important limitation to simple Capture Point formulations. Rotating the trunk or rapidly moving the legs can modify the relationship between center-of-mass motion and ground reaction forces. Advanced controllers can exploit this additional momentum authority rather than assuming it is negligible. The resulting generalized formulations provide greater recovery capability during aggressive quadruped maneuvers.

Variable center-of-mass height also affects the dynamics. The standard LIPM assumes constant height, but a quadruped frequently lowers or raises its body when traversing obstacles, absorbing impacts, climbing slopes, or preparing for jumps. Variable-height inverted-pendulum models and generalized DCM formulations can account for these motions, although they increase planning and control complexity.

Uneven terrain creates further challenges because future support surfaces may have different heights and orientations. A capture location that is valid on a flat horizontal plane may not correspond directly to a foothold on stairs, rocks, or slopes. Terrain-aware planners therefore combine DCM-based recovery requirements with perceived surface geometry, contact normals, friction estimates, collision constraints, and foothold quality.

State estimation accuracy is critical because DCM depends directly on center-of-mass velocity. Small velocity errors can significantly shift the estimated capture location, especially during fast locomotion. Reliable inertial sensing, joint-state estimation, contact detection, visual or LiDAR odometry, and dynamic filtering are therefore important for preventing unnecessary or incorrectly directed recovery steps.

Disturbance detection can be implemented by comparing the measured or estimated DCM with its desired trajectory. A growing DCM error indicates that the robot\'s dynamic state is diverging from the planned motion. Small errors may be corrected through contact-force redistribution, while larger deviations can trigger foothold adjustment, swing-time modification, gait transition, or emergency recovery stepping.

A practical controller should use thresholds carefully because reacting to every small DCM deviation can produce unnecessary stepping and oscillatory behavior. Dead bands, prediction of future error, confidence measures, and disturbance persistence can help determine whether force control is sufficient or contact replanning is required. This creates a graded recovery strategy instead of a simple stable-versus-unstable decision.

Payloads influence Capture Point and DCM behavior by changing the system center of mass, inertia, and feasible acceleration. A moving manipulator or shifting payload can additionally create internal momentum that changes balance requirements. For quadruped mobile manipulators, the balance controller should therefore estimate the combined robot-payload state rather than relying on nominal base parameters alone.

Gait selection also determines the available recovery mechanisms. During a slow crawl, multiple stance contacts provide substantial force-redistribution authority. During a trot, the support region may become narrow and stepping decisions become more important. Bounding, running, and flight phases rely even more strongly on predictive contact placement because continuous ground-force correction may temporarily be unavailable.

Capture Point and DCM should therefore be viewed as components of a broader balance architecture rather than isolated stability metrics. Support geometry determines where forces can act, friction determines which forces are feasible, kinematics constrain reachable footholds, and whole-body dynamics determine whether commanded actions can actually be produced. DCM provides a compact state linking these physical constraints to future recoverability.

In an integrated quadruped controller, state estimation provides center-of-mass position and velocity, DCM estimation identifies the evolving divergent state, and a predictive planner determines whether existing contacts can recover it. If necessary, footholds and timing are modified. A force or whole-body controller then realizes the required contact actions while respecting friction, torque, and kinematic constraints.

The principal advantage of Capture Point and DCM methods is that they transform balance from a purely positional question into a prediction of recoverability. The controller evaluates where the robot is moving, how rapidly its unstable state is evolving, and what future contact action can arrest that evolution. This is especially valuable for disturbance rejection and high-speed locomotion where static stability margins become insufficient.

By combining DCM regulation, capture-region analysis, contact-force optimization, and adaptive foot placement, a quadruped can respond to disturbances before falling becomes unavoidable. These concepts provide a bridge between instantaneous balance control and future contact planning, enabling the robot to exploit both its current support forces and its ability to create new contacts for robust dynamic locomotion.

## 05.04. Stance Phase Force Distribution Optimization [w/Code]

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

During the stance phase of quadruped locomotion, the feet in contact with the terrain must collectively generate the forces and moments required to support the robot and control its motion. Stance-phase force distribution determines how the desired whole-body wrench is divided among these contacts while satisfying friction, contact, actuator, and stability constraints.

The fundamental input to force distribution is usually a desired body wrench consisting of a resultant force and resultant moment. The force component supports gravity and produces desired center-of-mass acceleration, while the moment component regulates body orientation and angular momentum. Individual stance-foot forces must combine to approximate or exactly realize this commanded wrench.

For a robot with several stance feet, multiple combinations of contact forces may generate the same resultant body wrench. This redundancy makes force distribution an optimization problem rather than a unique algebraic solution. The controller can exploit the additional degrees of freedom to improve stability, reduce actuator effort, maintain friction margins, smooth contact loading, and prepare for upcoming gait transitions.

The relationship between contact forces and body wrench can be constructed from the location of each stance foot relative to the center of mass. Every contact force contributes directly to the resultant linear force and also generates a moment through its lever arm. Stacking these relationships produces a mapping from individual ground reaction forces to the net wrench acting on the robot.

A basic optimization objective minimizes the difference between the desired wrench and the wrench generated by the selected contact forces. Weighted penalties can assign different importance to linear acceleration, roll, pitch, and yaw regulation. Additional regularization terms can discourage unnecessarily large forces or abrupt changes from the forces calculated during the previous control cycle.

Ground contacts impose unilateral constraints because a normal stance force can push the robot away from the terrain but normally cannot pull it toward the ground. Consequently, each contact force must maintain an appropriate positive normal component while the foot is loaded. A foot scheduled for liftoff can progressively reduce this component until its commanded contact force approaches zero.

Friction is another fundamental constraint. The tangential contact force must remain sufficiently small relative to the normal force to prevent slipping. Coulomb friction is naturally represented by a friction cone, but real-time optimization frequently approximates this cone using linear inequalities forming a friction pyramid. Conservative margins can compensate for uncertain or spatially varying friction.

Force limits must also reflect actuator capability. Even when a contact force satisfies friction conditions, the corresponding joint torques may exceed motor, gearbox, thermal, or structural limits. A more complete optimizer therefore includes torque constraints directly or maps approximate feasible force ranges from the leg Jacobian and known actuator limits to prevent commands that cannot be physically realized.

The leg Jacobian provides the connection between Cartesian contact forces and joint torques. Under an appropriate quasi-static relationship, the transpose of the Jacobian maps foot force into generalized joint torque. This relationship allows the optimizer or subsequent whole-body controller to evaluate whether a proposed force distribution is compatible with the instantaneous leg configuration and available actuator authority.

Quadratic Programming, commonly abbreviated as QP, is widely used for stance-force optimization because many tracking objectives can be written as quadratic costs while friction, force, and torque restrictions can be represented by linear constraints or suitable approximations. Efficient QP solvers can compute force distributions at high control rates, making this formulation practical for real-time quadruped locomotion.

The weighting of the objective function strongly influences robot behavior. A high body-orientation weight may preserve trunk attitude aggressively but demand large or uneven contact forces. Strong force regularization produces smoother loading but may reduce tracking performance. Controller design therefore requires balancing motion accuracy, robustness, energy use, and available contact authority rather than minimizing a single physical quantity.

Load sharing provides an additional optimization objective. During symmetric standing on level terrain, approximately balanced vertical loading may be desirable. During acceleration, slope traversal, or manipulation, however, intentionally asymmetric loading may be necessary. The optimizer should therefore treat equal force distribution as a preference when appropriate rather than as a universal balance requirement.

Contact-force smoothing is particularly important near gait transitions. Immediately setting the force of a newly contacting foot to a large value can create impact-like behavior and excite structural vibration. Similarly, removing force abruptly before liftoff can disturb body motion. Force references are therefore commonly ramped according to the contact phase or penalized for rapid temporal variation.

During a crawl gait, three or four feet may support the body for substantial portions of the gait cycle, providing considerable redundancy for force allocation. The optimizer can maintain large friction and stability margins while transferring weight gradually between contacts. This makes force-distribution control relatively tolerant of moderate modeling errors and disturbances during slow locomotion.

Trotting presents a more demanding problem because diagonal pairs of feet frequently provide the primary support. With fewer simultaneous contacts, the set of achievable body wrenches becomes more restricted. The optimizer must prioritize essential balance objectives while respecting narrow force-feasibility margins, and body acceleration or orientation commands may need to be reduced when the desired wrench cannot be generated.

Bounding and running introduce even more rapid force variations and may include flight phases. Stance intervals become short, requiring relatively large impulses to redirect the body momentum. Optimization must consider peak force limits, contact duration, actuator bandwidth, and impact behavior. Force distribution in these regimes is therefore closely connected to trajectory optimization and predictive locomotion planning.

Terrain orientation changes the definition of normal and tangential contact forces. On a slope, force constraints should be expressed relative to the local terrain normal rather than a fixed world vertical direction. For irregular terrain, each foot may have a different contact frame. Accurate terrain-normal estimation is consequently important for constructing physically meaningful friction constraints.

Noncoplanar contacts can generate combinations of forces and moments unavailable on a flat surface, but they also complicate feasibility analysis. Direct contact-force optimization handles such configurations naturally because each force is expressed at its actual three-dimensional contact location. This is one reason modern quadruped controllers often prefer force- or wrench-based formulations over purely planar stability criteria.

Stability margins can be incorporated into optimization by discouraging solutions that operate close to friction boundaries, force limits, or support-region boundaries. Rather than merely satisfying constraints, the optimizer can retain reserve authority for disturbances. This reserve becomes especially valuable when terrain properties are uncertain or when state estimation and contact-location estimates contain errors.

Contact uncertainty can be addressed by modifying force limits according to confidence. A foot with uncertain contact quality should not immediately receive a large fraction of the body load. The controller can initially assign a conservative force bound and increase it after reliable contact is confirmed. Conversely, unexpected force loss or slip can trigger rapid redistribution to the remaining stance legs.

Model Predictive Control extends instantaneous force optimization by considering force distributions across future contact phases. Instead of selecting forces solely for the current state, MPC predicts how present forces influence future center-of-mass motion and orientation. It can therefore prepare for upcoming liftoff, touchdown, acceleration, or terrain changes while respecting the scheduled contact sequence.

Centroidal dynamics provide a useful model for predictive force optimization. The total linear momentum changes according to external forces, while angular momentum changes according to moments generated by those forces around the center of mass. Optimizing contact forces within this representation captures the dominant whole-body balance dynamics without requiring every joint state to appear in the high-level optimization.

Whole-Body Control can subsequently translate optimized contact forces into joint-level commands. The WBC simultaneously considers desired body acceleration, stance constraints, swing-leg tasks, joint limits, and torque capability. If the high-level force solution is dynamically inconsistent with detailed robot constraints, hierarchical or unified optimization can adjust the command while preserving the most important balance objectives.

Force estimation provides essential feedback for this process. Robots equipped with foot force sensors can directly measure ground reaction forces, while other platforms estimate them from joint torques, motor currents, actuator models, or observers. Comparing estimated and commanded forces allows the controller to detect contact errors, compensate for modeling inaccuracies, and identify potential slipping or unexpected terrain interaction.

Payloads significantly alter optimal force distribution. An asymmetric load shifts the combined center of mass, while a robotic manipulator can generate additional forces and moments during interaction. The stance controller should account for these effects when computing the desired body wrench. Otherwise, nominally symmetric force allocation can produce orientation errors or overload particular legs.

Energy and thermal considerations can also influence force allocation over longer operating periods. Repeatedly assigning high loads to the same leg may increase motor temperature and mechanical stress. Secondary optimization objectives can distribute effort according to actuator condition, efficiency, or thermal state while preserving the primary requirements of balance and trajectory tracking.

Force distribution should also coordinate with foothold planning. A poor foothold configuration may make the desired wrench difficult or impossible to generate regardless of optimization quality. Predictive locomotion systems therefore evaluate not only whether a foot location is kinematically reachable, but also whether the resulting contact arrangement provides sufficient force and moment authority for upcoming motion.

In practical implementations, stance-force optimization is executed repeatedly at high frequency as state estimates and contact conditions change. Each cycle updates the desired body wrench, active contact set, terrain frames, friction estimates, and physical limits. Warm-starting the solver from the previous solution can reduce computation and encourage temporal consistency, particularly in rapidly changing locomotion.

Robust force distribution does not seek merely to satisfy equilibrium at the current instant. It maintains feasible contact forces while preserving enough control authority to respond to disturbances and future gait changes. This requires combining wrench tracking, friction margins, actuator limits, contact confidence, temporal smoothing, and predictive information within a unified optimization framework.

Stance-phase force distribution optimization therefore forms a central bridge between high-level locomotion objectives and physical interaction with the terrain. By converting desired body motion into feasible forces at individual feet, it enables the quadruped to regulate center-of-mass motion, body orientation, and momentum while adapting continuously to gait, terrain, payload, and disturbances.

## 05.05. Push Recovery Controller Design [w/Code]

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

Push recovery is the capability of a quadruped robot to remain upright and return toward a controllable locomotion state after an unexpected external disturbance. A push can alter center-of-mass velocity, body orientation, angular momentum, and contact loading within a very short time. Effective recovery therefore requires rapid state estimation, disturbance assessment, force redistribution, and, when necessary, adaptive stepping.

A push-recovery controller should distinguish between small disturbances that can be rejected using existing contacts and larger disturbances that require changes in the contact configuration. This distinction prevents unnecessary stepping while preserving recovery capability. The controller can progressively escalate from posture and force regulation to foot-placement adjustment, gait modification, and emergency recovery actions as disturbance severity increases.

Disturbance detection begins with the estimated robot state. Unexpected changes in body velocity, angular velocity, orientation, momentum, contact forces, or tracking error can indicate external interaction. Rather than relying on a single signal, practical systems combine inertial measurements, joint states, contact-force estimates, and model predictions to distinguish genuine disturbances from normal locomotion dynamics and sensor noise.

An external-force observer can improve disturbance estimation by comparing measured robot behavior with the acceleration and momentum changes predicted by the dynamic model. The residual between expected and observed motion provides information about unmodeled external forces or moments. Accurate estimation is useful because the magnitude, direction, and duration of the disturbance strongly influence the appropriate recovery strategy.

For relatively small pushes, the robot can often recover without changing footholds. Ground reaction forces are redistributed among the active stance legs to generate corrective linear and angular accelerations. Body orientation feedback and center-of-mass regulation modify the desired whole-body wrench, while a force optimizer determines contact forces that realize this wrench without violating friction or actuator constraints.

The available recovery authority depends strongly on the current support configuration. Four-foot stance generally provides substantial force and moment capability, whereas a diagonal two-foot stance during trotting offers a much narrower feasible region. A recovery controller should therefore evaluate disturbance severity relative to the instantaneous contact configuration rather than applying a fixed threshold independent of gait phase.

Center-of-mass velocity is especially important because a robot can appear geometrically stable immediately after a push while possessing enough momentum to leave the support region shortly afterward. Capture Point or Divergent Component of Motion concepts provide compact measures combining position and velocity. These quantities help predict whether current contacts can arrest the motion or whether a new foothold must be created.

When force redistribution is insufficient, stepping becomes the primary recovery mechanism. A foot is placed in the direction required to enlarge or reposition the future support region. The desired recovery foothold depends on center-of-mass state, disturbance direction, available swing legs, kinematic reachability, terrain conditions, and contact timing. A feasible step must be both dynamically useful and physically reachable.

Recovery stepping is not limited to changing foot position. Swing timing can be equally important because an ideal foothold provides little benefit if contact occurs too late. The controller may accelerate an ongoing swing, shorten the remaining swing duration, delay another leg\'s liftoff, or select a different leg for recovery. Spatial and temporal replanning should therefore be coordinated.

A quadruped has several possible recovery legs, creating flexibility but also a discrete decision problem. The best leg depends on gait phase, disturbance direction, current foot locations, workspace limits, and terrain. Selecting the nearest leg is not always optimal. The controller should prefer a contact that provides sufficient recovery authority while avoiding self-collision, singular configurations, and excessive joint motion.

The capture region provides a useful representation for recovery-step planning. It describes foothold locations from which the disturbed state can be brought toward a bounded or stable condition. Intersecting this region with the leg\'s reachable workspace and safe terrain areas produces a set of candidate recovery contacts. Optimization can then select a foothold according to stability margin, effort, and future locomotion requirements.

Some disturbances cannot be recovered with a single step. Multi-step recovery becomes necessary when momentum is too large, the first reachable foothold is insufficient, or terrain limits available contacts. Predictive planning can generate a sequence of steps that progressively reduces divergent motion. The controller should avoid demanding complete recovery from the first step when several feasible contacts provide a safer solution.

Body attitude control is another essential recovery mechanism. A lateral push may produce both translational motion and roll angular momentum, while a longitudinal disturbance can generate pitch rotation. The controller should coordinate center-of-mass acceleration and body torque rather than treating them independently. Appropriate trunk rotation can sometimes increase the range of feasible recovery actions by exploiting angular momentum.

Centroidal dynamics provide a useful model for this coordination because they represent the evolution of total linear and angular momentum under external contact forces. A centroidal recovery planner can determine how stance forces and future contacts should redirect the disturbed momentum. This representation captures important whole-body effects while remaining computationally simpler than full rigid-body dynamics.

Model Predictive Control is well suited to push recovery because recovery is fundamentally a future-feasibility problem. MPC can predict center-of-mass motion, body orientation, contact forces, and upcoming contact transitions over a finite horizon. The optimizer can determine whether current contacts are sufficient and can prepare future forces or footholds before the robot reaches an unrecoverable state.

A recovery MPC should incorporate realistic constraints. Contact forces must remain inside friction limits, normal forces must satisfy unilateral contact conditions, joint torques should remain achievable, and recovery footholds must lie within kinematic workspaces. Including these constraints prevents the planner from producing mathematically stabilizing trajectories that the physical robot cannot execute.

Friction uncertainty is particularly important during push recovery because corrective forces may approach the available traction limit. Aggressively commanding horizontal force on a low-friction surface can convert a manageable disturbance into foot slip. Robust controllers therefore retain friction margins, estimate contact quality, and reduce reliance on contacts whose measured behavior suggests insufficient traction.

Slip detection should immediately modify the recovery strategy. A slipping foot should not continue to receive the load predicted for a rigid contact. The controller can reduce tangential force on that leg, redistribute load to reliable contacts, adjust body motion, or initiate a new step. Fast contact-state adaptation is essential because the feasible wrench region changes as soon as a contact loses traction.

Whole-Body Control converts recovery objectives into joint-level commands. Desired body acceleration, orientation, contact forces, and swing-foot trajectories must be coordinated while respecting joint limits and actuator capability. Task priorities may change temporarily during severe disturbances so that balance recovery receives higher priority than nominal velocity tracking, posture preferences, or secondary manipulation objectives.

Recovery behavior should be graded rather than binary. Small disturbances can be handled through impedance and force modulation, moderate disturbances through aggressive force redistribution and swing adjustment, and large disturbances through stepping or gait transition. Extreme disturbances may require protective actions when upright recovery is no longer physically feasible. Such escalation improves both efficiency and robustness.

Threshold selection should account for the robot\'s current dynamic state. A fixed body-angle or velocity threshold can perform poorly because identical measurements may imply different risks during standing, crawling, trotting, or running. Recovery triggers based on predicted feasibility, DCM error, capture-region boundaries, or remaining force authority provide more meaningful criteria than isolated state thresholds.

Gait adaptation can substantially increase recovery capability. A trotting robot may temporarily transition toward a wider or longer-duration support pattern after a disturbance. The controller can extend stance duration, insert an additional contact, reduce commanded velocity, or switch to a more conservative gait. Recovery therefore includes modification of locomotion structure, not merely correction of individual foot trajectories.

Terrain perception should participate in recovery planning whenever sufficient sensing and computation are available. A dynamically ideal recovery location may contain an obstacle, hole, steep surface, or low-friction material. Candidate footholds should therefore be filtered using terrain height, slope, roughness, semantic hazards, collision constraints, and estimated contact quality before they are accepted by the balance planner.

State-estimation latency strongly affects recovery performance. Push disturbances evolve quickly, and delayed velocity or orientation estimates can cause the controller to react after the feasible recovery region has already contracted. High-rate inertial sensing, accurate contact detection, low-latency filtering, and predictive estimation are therefore as important as the optimization algorithm itself.

Actuator bandwidth and torque limits determine how rapidly corrective forces can actually be generated. A controller designed without these limits may request instantaneous force changes that the hardware cannot follow. Recovery planning should account for torque-rate limits, motor saturation, transmission compliance, communication delay, and thermal restrictions so that predicted recovery authority reflects the real platform.

Payloads and manipulators can significantly alter recovery dynamics. An elevated payload raises the combined center of mass and may increase tipping sensitivity, while an extended manipulator changes inertia and can generate additional angular momentum. Recovery control should use the combined robot-payload state and, when possible, coordinate manipulator motion with leg actions to improve whole-body stabilization.

Learning-based methods can complement model-based push recovery by adapting policies to complex disturbances and uncertain dynamics. Reinforcement learning can expose the robot to varied push directions, magnitudes, timings, terrain conditions, and model parameters in simulation. However, learned recovery should still respect physical safety constraints, contact feasibility, and actuator limits when transferred to real hardware.

Domain randomization and disturbance curricula can improve robustness during training. The simulated robot can experience variations in mass, friction, latency, motor strength, payload, sensor noise, and external impulses. Training can gradually increase disturbance severity so that the policy learns both nominal stabilization and recovery behavior. Model-based safety layers can further constrain learned actions during deployment.

Push-recovery performance should be evaluated using more than whether the robot falls. Useful measures include maximum recoverable impulse, recovery time, number and length of recovery steps, peak contact force, friction margin, body-angle excursion, actuator saturation, and deviation from the original trajectory. Repeated tests across different gait phases reveal whether performance depends excessively on a favorable contact configuration.

A robust test protocol should apply disturbances from multiple directions and at different body locations because identical force magnitudes can generate different combinations of linear and angular momentum. Tests should also vary gait phase, terrain friction, payload, commanded velocity, and contact configuration. This produces a recovery envelope describing the range of disturbances that the robot can reliably withstand.

The overall push-recovery architecture is most effective when perception, estimation, prediction, force control, and footstep planning operate as a coordinated system. Disturbance estimation identifies what changed, dynamic-state analysis determines whether current contacts remain sufficient, predictive planning selects a recovery strategy, and whole-body control executes the required forces and motions.

Push recovery ultimately represents the ability to preserve recoverability rather than merely restore a nominal pose. A capable quadruped continuously evaluates whether its momentum can still be redirected using available contacts and reachable future footholds. By combining force redistribution, DCM or capture analysis, predictive stepping, gait adaptation, and whole-body optimization, the robot can respond to disturbances before falling becomes unavoidable.

## 05.06. Base Height and Roll Pitch Regulation [w/Code]

![](images/image6.png){width="7.268055555555556in" height="7.268055555555556in"}

Base height and roll-pitch regulation are fundamental components of quadruped balance control because the floating body must maintain a suitable pose while the legs repeatedly change contact with the terrain. The controller regulates vertical body position and trunk orientation so that the robot preserves leg workspace, contact quality, sensor alignment, and dynamic stability throughout locomotion.

Base height represents the vertical position of the robot body relative to the terrain or a selected support reference. The desired height is not simply a cosmetic posture parameter. It determines available leg extension, joint configuration, ground clearance, potential energy, and the range of vertical forces that the stance legs can generate without approaching kinematic or actuator limits.

If the body is maintained too high, the legs may become nearly fully extended and lose useful workspace for rejecting disturbances or following uneven terrain. If it is too low, joints may approach folded configurations, the body may collide with obstacles, and available motion for absorbing impacts can decrease. Height regulation therefore maintains an operating region that preserves sufficient motion in both directions.

Roll describes rotation of the base about its longitudinal axis, while pitch describes rotation about the lateral axis. These orientations strongly influence balance because excessive roll or pitch shifts the distribution of load among the legs and can move the combined center of mass toward critical support boundaries. Orientation regulation generates corrective moments through coordinated stance-leg forces.

The desired roll and pitch are not always zero. On flat terrain, maintaining an approximately level trunk is often useful for sensing, payload stability, and predictable locomotion. On slopes or structured obstacles, however, the desired body orientation may follow the terrain partially or remain closer to the gravity-level frame depending on the task, leg workspace, friction conditions, and sensor requirements.

A terrain-aligned posture can preserve more symmetric leg configurations when traversing a long slope. In contrast, keeping the body closer to horizontal may be desirable for payloads or perception sensors that require a stable gravity-referenced orientation. Practical controllers therefore generate desired roll and pitch from a combination of terrain geometry, locomotion objectives, mechanical limits, and mission requirements.

Terrain orientation can be estimated from stance-foot locations or perception measurements. A support plane may be fitted to the active contacts, providing an approximate local surface normal. Vision, depth sensing, or LiDAR can additionally estimate upcoming slope before the feet establish contact. Combining contact-based and perception-based estimates allows body posture to respond smoothly rather than reacting only after terrain changes.

Base height can similarly be referenced to an estimated terrain plane instead of a fixed world-coordinate altitude. This is important when climbing ramps, stairs, or irregular surfaces because a constant global vertical coordinate would not preserve consistent leg extension. The desired body position can be generated as an offset above the local support surface while maintaining sufficient clearance from terrain obstacles.

State estimation provides the feedback required for pose regulation. An inertial measurement unit supplies orientation and angular velocity, while joint encoders and forward kinematics estimate foot positions relative to the base. Contact information identifies which feet can be trusted as support references. Sensor fusion combines these measurements to estimate body height, vertical velocity, roll, pitch, and their rates.

Direct differentiation of estimated height or orientation can amplify noise, so velocity estimates normally require filtering or observer-based estimation. Excessive filtering, however, introduces phase delay that can reduce balance performance. The estimator and controller bandwidths should therefore be designed together so that the pose loop reacts rapidly to disturbances without responding strongly to measurement noise or structural vibration.

A simple base-height controller can use proportional and derivative feedback on vertical position and velocity. Height error generates a desired vertical acceleration or force, while vertical-velocity feedback provides damping. Gravity compensation supplies the nominal force required to support the robot. The resulting total vertical-force command is then distributed among the active stance legs.

Roll and pitch can be regulated in a similar feedback structure using orientation error and angular velocity. The controller computes desired body moments that oppose rotational deviation and provide damping. These moments are realized by creating appropriate differences in stance-leg forces. Increasing force on one side while decreasing it on the opposite side, for example, can generate a corrective roll moment.

Orientation errors require careful representation because three-dimensional rotations are not ordinary Euclidean vectors. For moderate roll and pitch deviations, simple angle errors may be adequate, but more general controllers use rotation matrices, quaternions, or Lie-group representations. These methods avoid singularities and provide consistent orientation errors during larger body rotations or complex terrain traversal.

The desired vertical force and roll-pitch moments together form part of the desired body wrench. A stance-force optimizer distributes this wrench among the available contacts while satisfying friction, unilateral-force, and actuator constraints. This coupling is important because height and attitude cannot be regulated independently of the physical forces that the terrain contacts can actually generate.

Contact geometry determines how effectively stance forces can regulate orientation. A wide lateral stance provides strong roll-moment authority, while a long fore-aft separation improves pitch control. When only two diagonal feet support the robot during a trot, the achievable moment set becomes more restricted. Controller gains and priorities may therefore need to vary with the active contact configuration.

Force distribution should avoid regulating pose so aggressively that it drives contacts toward friction or actuator limits. A large roll error does not justify a corrective moment that causes a foot to slip or overloads a leg. Optimization-based controllers can soften pose tracking when constraints become active, preserving contact feasibility and overall balance before attempting to restore the nominal body pose.

Base-height regulation is closely related to vertical compliance. A perfectly rigid height controller can transmit terrain impacts directly into the body and demand large contact-force changes. Introducing controlled compliance through impedance behavior allows the base to move slightly in response to impacts while returning toward the reference afterward. This improves shock absorption and reduces peak forces.

An impedance formulation commonly relates vertical position and velocity errors to desired restoring force, producing behavior analogous to a virtual spring and damper. Similar rotational impedance can be applied to roll and pitch. The virtual stiffness determines how strongly the body returns toward its desired pose, while virtual damping controls oscillation and energy dissipation after disturbances.

Controller gains should depend on robot mass, inertia, gait, actuator bandwidth, and contact conditions. Excessive stiffness can create oscillation or force saturation, whereas insufficient stiffness produces large body excursions. Derivative gains that are too high may amplify sensor noise. Gain scheduling can adapt these parameters according to gait phase, speed, terrain, payload, and number of stance contacts.

Height commands can also be planned proactively. The robot may lower its body before accelerating rapidly to increase stability margin, raise the base to cross an obstacle, or crouch before jumping to create additional leg extension for propulsion. Thus, base-height regulation should track a planned trajectory rather than always enforcing a single fixed nominal value.

Roll and pitch references can likewise support locomotion objectives. During rapid turning or lateral acceleration, a controlled body lean may improve force distribution and reduce required lateral contact force. During uphill motion, a planned pitch adjustment can preserve leg workspace and improve traction. Orientation regulation should therefore distinguish intentional reference motion from unwanted attitude disturbance.

Swing-leg motion interacts with base regulation because moving a leg changes the robot\'s internal momentum and mass distribution. Rapid swing acceleration can produce reaction forces and moments on the trunk. Whole-body controllers can anticipate these effects and adjust stance forces so that base height and orientation remain controlled without requiring large corrective action after the disturbance occurs.

Payloads introduce additional challenges because they shift the combined center of mass and change body inertia. An asymmetric payload can create persistent roll or pitch moments, while a moving manipulator can generate time-varying disturbances. Pose regulation should use updated mass properties or online estimates so that feedforward wrench calculations remain consistent with the actual robot configuration.

Manipulation tasks may intentionally modify the posture objective. A quadruped carrying a robotic arm may lower its body and widen its stance before applying a large manipulation force. Roll and pitch references can be adjusted to counter expected reaction moments. In this case, locomotion balance and manipulation stability become a single whole-body force-control problem.

Uneven terrain makes independent regulation of every body variable impractical because strict height and orientation tracking can conflict with foot-contact constraints. The controller should prioritize stable contact and feasible leg configuration over exact pose tracking. Soft optimization objectives allow the body to deviate moderately from the nominal reference when necessary to maintain reliable support.

Joint limits must be considered when selecting the desired base pose. Even if a body height is dynamically stable, it may place one or more legs close to kinematic limits on irregular terrain. Online posture optimization can adjust height, roll, and pitch simultaneously to maximize workspace margin while maintaining sufficient ground clearance and acceptable body orientation.

Model Predictive Control can optimize future base pose together with contact forces and footholds. By predicting upcoming terrain and contact transitions, MPC can begin changing height or orientation before a difficult step occurs. This reduces sudden corrections and allows the robot to prepare its leg workspace for stairs, slopes, gaps, or large changes in terrain elevation.

Whole-Body Control provides the final coordination between base regulation and leg tasks. Desired base acceleration, angular acceleration, stance forces, and swing-foot trajectories are solved together subject to robot dynamics and joint constraints. Task weighting or hierarchy ensures that contact consistency and balance remain dominant when exact height or orientation tracking becomes temporarily infeasible.

Disturbance recovery may require temporary relaxation of nominal pose regulation. After a strong push, aggressively forcing the trunk immediately back to its original roll or pitch can conflict with the motion required to regain balance. A recovery controller may allow transient body lean while prioritizing momentum regulation and stepping, then gradually restore the nominal base pose after the dynamic state becomes recoverable.

Performance can be evaluated using height tracking error, roll-pitch error, angular-rate response, settling time, contact-force variation, joint-limit margin, and disturbance rejection. Tests should include standing, gait transitions, slopes, uneven terrain, payload variation, and external pushes. Evaluation across multiple conditions reveals whether the controller is robust rather than merely tuned for level-ground standing.

Base height and roll-pitch regulation therefore serve as more than simple posture-control functions. They coordinate body geometry, contact-force capability, leg workspace, terrain adaptation, and disturbance response. When integrated with state estimation, force optimization, predictive planning, and whole-body control, they provide a stable and adaptable body platform for reliable quadruped locomotion.

## 05.07. Three Legged Stand and Fault Tolerant Balance [w/Code]

![](images/image7.png){width="7.268055555555556in" height="7.268055555555556in"}

Three-legged standing is an important capability for a quadruped robot because normal locomotion repeatedly requires one leg to leave the ground while the remaining three support the body. The same capability also provides a foundation for fault-tolerant balance when one leg becomes unavailable because of actuator failure, mechanical damage, sensor faults, poor terrain contact, or deliberate maintenance operations.

When three feet remain in contact, their contact locations approximately define a triangular support region on planar terrain. For static equilibrium, the vertical projection of the combined center of mass should remain inside this triangle with an adequate stability margin. The robot can shift its body before unloading the fourth leg so that the center of mass moves toward a safer location within the remaining support region.

The support triangle is generally smaller and more asymmetric than the four-leg support polygon. Consequently, the available margin against tipping decreases and the body becomes more sensitive to disturbances, payload shifts, and contact-position errors. The controller should therefore evaluate not only whether the center-of-mass projection lies inside the triangle, but also how far it remains from each critical support edge.

Three-legged balance is fundamentally a whole-body coordination problem. Moving the trunk changes the center-of-mass location, while modifying base height, roll, and pitch changes leg geometry and force capability. The controller should select a body pose that simultaneously preserves static or dynamic stability, adequate joint workspace, ground clearance, and feasible force generation at all three supporting legs.

Before intentionally lifting a leg, the controller should perform a load-transfer phase. The commanded contact force on the departing foot is gradually reduced while the remaining three feet assume additional load. This transition avoids a sudden change in the resultant ground reaction force and allows the controller to verify that the three-leg contact configuration can support the body before the foot completely leaves the surface.

Force distribution becomes less redundant after one contact is removed. With four stance legs, several combinations of contact forces may realize the desired body wrench. Three contacts still provide significant control authority, but the feasible force and moment set becomes smaller. The optimizer must prioritize essential balance objectives while respecting unilateral-force, friction, actuator, and joint-torque constraints.

The geometric center of the support triangle is not necessarily the optimal center-of-mass target. Terrain friction, leg configuration, actuator capability, payload distribution, and expected disturbances can make one part of the support region safer than another. Optimization can therefore select a desired body position that maximizes practical stability and force margins rather than simply centering the body geometrically.

Friction constraints become particularly important because each remaining leg carries a larger fraction of the total load. On a slope or low-friction surface, the tangential force required from one stance foot may approach its friction limit. A fault-tolerant controller should retain conservative friction margins and avoid redistributing load in a way that converts a single-leg problem into slip at another contact.

Terrain geometry also influences three-legged stability. If the supporting feet lie at different heights or on surfaces with different orientations, a simple horizontal support triangle may provide an incomplete description. The controller can use three-dimensional contact positions, local surface normals, contact wrench feasibility, and centroidal dynamics to determine whether the remaining contacts can generate the required support forces and moments.

Fault-tolerant balance begins with reliable fault detection and isolation. A controller must determine whether abnormal behavior originates from an actuator, encoder, force sensor, communication link, mechanical transmission, or terrain contact. Incorrectly declaring a healthy leg failed reduces available support unnecessarily, while continuing to rely on a genuinely failed leg can rapidly destabilize the robot.

Fault indicators may include unexpected joint-position error, torque-tracking error, abnormal motor current, temperature increase, communication loss, inconsistent encoder measurements, or disagreement between expected and measured contact forces. Combining multiple indicators improves diagnostic reliability. Model-based residuals can additionally reveal when a leg no longer produces the motion or force predicted by the commanded input.

Not all failures require complete removal of a leg from control. A degraded actuator may still provide limited torque, a damaged sensor may be replaced by an observer estimate, or a slipping foot may regain contact after repositioning. Fault management should therefore distinguish healthy, degraded, unreliable, and unavailable states instead of representing every abnormal condition as a binary leg failure.

Once a fault is confirmed, the controller should reconfigure its contact and actuation model. The affected leg may be assigned zero support force, restricted torque limits, reduced task priority, or a safe holding posture. The stance-force optimizer and whole-body controller must then recompute feasible actions using only the remaining reliable capabilities rather than continuing to solve the nominal four-leg problem.

The immediate response to a sudden leg failure depends on the robot\'s dynamic state. During quiet standing, the controller may shift the center of mass slowly into the remaining support triangle. During walking or trotting, however, momentum may already be directed toward the failed side. Rapid force redistribution, body motion, or an emergency step may be required before a stable three-legged support configuration can be established.

Capture Point or Divergent Component of Motion analysis can assist this transition by determining whether the current center-of-mass position and velocity are recoverable using the remaining contacts. If the divergent state cannot be captured inside the three-leg support region, the robot should create a new contact or reposition an available foot instead of attempting to preserve the original stance geometry.

A failed leg also changes the reachable set of future contacts. Normal gait patterns based on alternating four-leg participation may no longer be possible. The locomotion planner must generate a fault-adapted contact sequence using the three functional legs. Depending on robot geometry and failure location, this may resemble a slow crawl, repeated hopping support transitions, or highly asymmetric stepping.

Three-legged locomotion is substantially more difficult than three-legged standing because each functional leg must alternate between supporting the body and creating the next contact. At certain moments only two reliable contacts may remain, requiring dynamic balance. A practical fault-tolerant system may therefore reduce commanded speed, increase stance duration, lower the body, and use conservative footholds to expand recovery margins.

The unavailable leg should normally be placed in a mechanically safe configuration. If possible, it can be folded or held away from the ground to prevent unintended collision, dragging, or snagging. However, the selected posture must not shift the center of mass excessively or interfere with the workspace of the remaining legs. Mechanical damage may further restrict which configurations are safe.

Base-height adaptation can improve fault tolerance. Lowering the body generally reduces the gravitational potential associated with tipping and can increase practical stability, although excessive lowering may reduce leg workspace. Roll and pitch references can also be adjusted so that the remaining legs operate in stronger configurations and the combined center of mass is positioned favorably relative to the support contacts.

Payload distribution becomes especially important after a leg failure. A payload located near the failed corner can shift the center of mass toward the missing support and substantially reduce the remaining stability margin. If the payload is movable, a manipulator or internal mechanism may reposition it. Otherwise, the base posture and surviving contact forces must compensate for the asymmetric mass distribution.

Model Predictive Control can evaluate whether three-legged balance remains feasible over future contact transitions. The prediction model can exclude or constrain the failed leg while optimizing center-of-mass motion, body orientation, contact forces, and available footholds. This allows the controller to prepare for future reductions in support rather than responding only after each contact transition occurs.

Whole-Body Control provides the mechanism for executing the reconfigured strategy. The controller coordinates desired base acceleration, stance forces, functional-leg motion, and the safe posture of the damaged leg while respecting the modified torque and kinematic limits. Task priorities should be adjusted so that balance and contact integrity dominate nominal speed tracking or secondary objectives.

Fault tolerance should also address sensing failures that do not directly remove mechanical support. If an encoder fails while the actuator remains functional, state estimation may reconstruct the missing information from redundant sensors or dynamic observers. Similarly, failure of a foot-force sensor does not necessarily require abandoning the contact if reliable force estimates can be obtained from actuator torques and robot dynamics.

Communication faults require special treatment because the controller may lose both sensing and command authority for an affected actuator. A local joint controller should ideally enter a predefined safe state when communication is lost. The higher-level balance controller must rapidly update its model so that it does not assume that commanded torques or positions are being executed by the disconnected subsystem.

Fault-tolerant control should preserve reserve capability rather than operating continuously at the physical limits of the three remaining legs. If all available friction and torque capacity is consumed merely to maintain nominal posture, even a small secondary disturbance can cause failure. Conservative body positioning and force allocation maintain residual authority for unexpected pushes, terrain errors, and modeling uncertainty.

Recovery from a temporary fault requires controlled reintegration. A leg that becomes available again should not immediately receive its nominal share of load. The controller should verify actuator health, establish reliable contact, gradually increase force, and monitor consistency between commanded and measured behavior. This prevents an intermittent fault from destabilizing the robot during re-entry.

Testing three-legged and fault-tolerant balance requires systematic failure injection. Experiments can disable one leg at a time during standing, gait transitions, and locomotion while varying terrain, payload, and disturbance conditions. Both planned leg removal and unexpected failure should be tested because the latter provides little time for anticipatory center-of-mass shifting.

Useful evaluation metrics include minimum stability margin, maximum recoverable disturbance, peak force in surviving legs, actuator saturation, body-angle excursion, recovery time, and the duration for which three-legged support can be maintained. Fault-detection delay and false-alarm rate are equally important because even an excellent recovery controller depends on timely and correct diagnosis.

Different failed-leg locations should be tested independently because front and rear legs influence pitch authority differently, while left and right failures alter lateral stability. Mechanical and payload asymmetry can further produce different behavior for each corner. A robust controller should therefore adapt to the identity of the unavailable leg rather than using one fixed compensation strategy.

Three-legged standing demonstrates that quadruped stability depends on adaptable use of contact geometry rather than simply maintaining four feet on the ground. By shifting the center of mass, redistributing forces, adjusting body pose, and respecting reduced feasibility margins, the robot can maintain useful balance despite the loss of one nominal support contact.

Fault-tolerant balance extends this principle into a complete resilience architecture combining diagnosis, model reconfiguration, force optimization, predictive planning, and whole-body control. When these components operate together, a quadruped can degrade its performance gracefully instead of failing immediately, preserving stability and potentially continuing limited locomotion even after significant loss of leg capability.

## 05.08. External Disturbance Estimation and Rejection [w/Code]

![](images/image8.png){width="7.268055555555556in" height="7.268055555555556in"}

External disturbance estimation and rejection allow a quadruped robot to identify forces and moments that are not predicted by its nominal motion model and compensate for them before they develop into loss of balance. Disturbances may originate from pushes, payload interaction, wind, impacts, terrain irregularities, slipping contacts, modeling errors, or unexpected physical interaction with the environment.

A disturbance affects the robot through changes in linear and angular momentum. An external force modifies center-of-mass acceleration, while an external moment changes angular momentum and body orientation. Because these effects can occur rapidly, the balance controller requires an estimate not only of the robot state but also of the unexplained wrench acting on the floating base.

The robot dynamics provide a natural basis for disturbance estimation. Measured joint motion, estimated base acceleration, commanded actuator torque, gravity, and modeled contact forces can be compared with the behavior predicted by the rigid-body model. The residual between predicted and observed dynamics contains information about external forces, unmodeled contacts, actuator errors, and modeling uncertainty.

A generalized momentum observer is a common approach for estimating disturbances. Instead of differentiating noisy velocity measurements directly, the observer tracks the evolution of generalized momentum and compares it with the momentum change expected from known forces and torques. The resulting residual can represent an equivalent external generalized force acting on the robot.

Centroidal momentum provides another useful representation for quadruped balance. The rate of change of total linear momentum depends on gravity and external forces, while angular momentum changes according to moments generated by contact forces and external interaction. A mismatch between measured momentum evolution and predicted contact contributions can therefore indicate an unknown external wrench.

The accuracy of disturbance estimation depends strongly on state estimation. Errors in base velocity, orientation, angular velocity, joint motion, or contact state can appear as false disturbances. High-rate inertial measurements, accurate joint encoders, reliable contact detection, and consistent kinematic estimation are therefore essential before the residual of the dynamic model can be interpreted as an external interaction.

Contact-force information is particularly important because normal locomotion already produces large and rapidly changing ground reaction forces. If these forces are measured directly by foot sensors, they can be included in the disturbance model. When direct sensing is unavailable, contact forces may be estimated from actuator torque, joint dynamics, motor current, or a whole-body observer.

Contact transitions create a major challenge for disturbance observers. Touchdown and liftoff naturally generate rapid changes in force and momentum that can resemble external impacts. The estimator should use the planned contact schedule and detected contact state to distinguish expected locomotion events from unexpected disturbances. Observer gains may also be adjusted around transitions to prevent false detections.

Disturbance estimation can be expressed as a six-dimensional external wrench consisting of three force components and three moment components. Estimating the complete wrench is useful because two disturbances with similar force magnitude can have very different effects when applied at different body locations. A force acting far from the center of mass can generate substantial rotational motion.

The estimated wrench does not always identify the exact point of application. Additional assumptions or measurements are required to localize the disturbance. Tactile sensors, force sensors, collision detectors, or manipulator measurements can provide contact-location information. Without such information, the controller can still use the equivalent wrench at the center of mass for balance compensation.

Observer bandwidth determines how quickly the estimator responds. A high-bandwidth observer can detect sudden pushes rapidly but becomes more sensitive to sensor noise, model errors, and contact impacts. A low-bandwidth observer produces smoother estimates but may react too slowly for dynamic balance. Practical designs therefore balance detection latency against noise sensitivity and may use adaptive filtering.

Bias compensation is important because persistent modeling errors can otherwise appear as constant external forces. Incorrect robot mass, payload location, center-of-mass position, joint friction, or actuator calibration can produce systematic residuals. Slowly varying bias terms can be estimated separately so that the disturbance observer remains sensitive to genuine environmental interaction rather than permanent model mismatch.

Once a disturbance has been estimated, the controller must determine whether it should be rejected. Not every external force is undesirable. A manipulator pressing against a surface, towing a load, or intentionally leaning against an object creates an external wrench that belongs to the task. Disturbance rejection must therefore distinguish intended interaction from uncommanded disturbance.

For small disturbances, rejection can be achieved by modifying the desired body wrench while maintaining the existing contact configuration. If an estimated horizontal force pushes the robot laterally, the controller can command an opposing center-of-mass acceleration and corrective body moment. A stance-force optimizer then distributes the required compensation among the supporting feet.

Feedforward disturbance compensation can improve response speed. Instead of waiting for position or orientation errors to grow, the estimated external wrench can be directly counteracted in the desired wrench command. Feedback regulation remains necessary because disturbance estimates are imperfect, but feedforward compensation reduces the amount of body motion required before corrective action begins.

Force compensation must respect contact feasibility. The theoretically ideal opposing force may exceed the available friction or normal-force limits of the stance feet. The controller should therefore project compensation demands into the feasible contact-wrench region or solve an optimization problem that trades disturbance rejection against friction margin, actuator limits, and balance requirements.

A disturbance can also be rejected through body motion rather than direct force cancellation. Allowing controlled center-of-mass displacement or trunk rotation may reduce the required contact forces and preserve stability. This is especially important for large pushes, where attempting to hold the original body pose rigidly can consume available control authority and cause foot slip or actuator saturation.

Impedance control provides a natural framework for compliant disturbance rejection. The body can behave like a virtual mass-spring-damper system, yielding slightly under external force while generating restoring motion. Appropriate stiffness and damping allow the robot to absorb disturbance energy instead of opposing every interaction with maximum force.

The optimal compliance depends on the task and terrain. High stiffness may be useful when carrying a sensitive payload or maintaining precise sensor orientation, while lower stiffness can improve robustness to impacts and uncertain contacts. Variable impedance allows the controller to modify body stiffness and damping according to gait, disturbance severity, payload, and contact confidence.

When the disturbance exceeds the rejection capability of the current contacts, the strategy must change from force compensation to recovery motion. Capture Point or Divergent Component of Motion analysis can determine whether the disturbed center-of-mass state remains recoverable without stepping. If not, the controller should modify footholds or initiate a recovery step.

Model Predictive Control can combine disturbance estimation with future balance prediction. The estimated external wrench can be included in the prediction model so that future center-of-mass motion and contact forces reflect the disturbance. MPC can then optimize force redistribution, body motion, and upcoming footholds over a finite horizon rather than reacting only to instantaneous tracking error.

Persistent disturbances require different treatment from short impulses. A brief push primarily changes momentum, whereas a sustained force creates a continuing load that must be balanced over time. The estimator should characterize disturbance duration, and the controller may need to shift the nominal center of mass, modify body orientation, or change footholds to establish a new sustainable equilibrium.

Unknown payload forces can be interpreted as persistent disturbances until the payload model is updated. If a robot picks up an object, the additional weight and shifted center of mass initially produce model residuals. Online mass and center-of-mass estimation can convert this apparent disturbance into an updated nominal model, allowing the disturbance observer to focus again on unexpected interaction.

Slip creates a special disturbance-estimation problem because the assumed contact model itself becomes invalid. Unexpected body motion may initially appear as an external force even though the true cause is loss of ground constraint. Combining disturbance residuals with foot velocity, friction estimates, and contact-force consistency helps distinguish external pushing from contact slip.

Terrain impacts can similarly produce short, high-frequency residuals. A foot striking an obstacle or landing earlier than expected generates an impulsive interaction that should not always trigger aggressive whole-body rejection. Event classification can separate expected impact, unexpected collision, sustained external force, and loss of contact so that each condition receives an appropriate response.

Whole-Body Control coordinates disturbance rejection with locomotion tasks. The estimated wrench can modify desired base acceleration or contact-force objectives while the WBC simultaneously manages stance constraints, swing trajectories, joint limits, and torque limits. During strong disturbances, balance tasks can temporarily receive higher priority than nominal velocity or posture tracking.

Actuator saturation should be monitored during rejection because a mathematically feasible body wrench may still demand excessive joint torque. The mapping from contact force to joint torque depends on leg configuration, so disturbance authority changes continuously during locomotion. A robust controller should estimate remaining torque reserve before committing to aggressive compensation.

Faults and disturbances must also be distinguished. A motor that unexpectedly loses torque can produce motion similar to an external push, while an encoder error can create an apparent dynamic residual. Diagnostic logic should combine disturbance estimates with actuator health, communication status, sensor consistency, and contact information before selecting the recovery action.

Learning-based estimators can complement model-based observers when complex friction, actuator dynamics, compliance, or terrain interaction are difficult to model accurately. A learned residual model can estimate systematic prediction errors from robot data. However, the estimator should remain bounded and interpretable enough that erroneous predictions cannot directly generate unsafe compensating forces.

Disturbance observers should be validated with controlled force application. Known pushes can be applied in longitudinal, lateral, and vertical directions and at different body locations. Comparing the applied force with the estimated wrench reveals estimation delay, amplitude error, directional error, bias, and sensitivity to the point of application.

Validation should also include locomotion without external disturbances. The observer must not repeatedly interpret normal gait dynamics, touchdown impacts, acceleration commands, or model uncertainty as pushes. False-positive disturbance detection can degrade locomotion because the controller may generate unnecessary corrective forces against motions that were intentionally commanded.

Useful performance metrics include wrench estimation error, detection latency, rejection time, peak center-of-mass displacement, body-angle excursion, contact-force margin, actuator saturation, and maximum rejectable disturbance. Testing across standing, walking, trotting, slopes, irregular terrain, and payload conditions reveals how observer accuracy and rejection authority vary with operating state.

External disturbance estimation and rejection therefore form a closed loop between physical interaction and balance control. The estimator identifies unexplained forces and moments, the controller determines whether they represent unwanted disturbance, and the force or motion planner selects a feasible response using the available contacts and actuator authority.

A robust quadruped should not merely react after a disturbance creates large posture error. By observing momentum and dynamic residuals, estimating the external wrench, and incorporating that estimate into force optimization, predictive control, and recovery planning, the robot can respond at the level of the physical cause and preserve balance under uncertain real-world interaction.

## 05.09. Balance Recovery from Near Fall State [w/Code]

![](images/image9.png){width="7.268055555555556in" height="7.268055555555556in"}

A near-fall state occurs when a quadruped approaches the boundary of recoverable balance but has not yet entered an unavoidable fall. The center of mass may be moving rapidly outside the current support region, the trunk may have accumulated large angular momentum, or one or more contacts may be losing effectiveness. Recovery requires recognizing this condition early and using the remaining control authority decisively.

Near-fall recovery differs from ordinary balance regulation because restoring the nominal posture is no longer the immediate objective. The primary goal is to preserve recoverability by redirecting momentum, creating useful contacts, and preventing body-ground collision. Temporary deviations in body position, orientation, gait, and commanded velocity are acceptable if they enlarge the set of dynamically feasible recovery actions.

A geometric stability criterion alone is insufficient for detecting a near fall. The center-of-mass projection may still lie inside the support polygon while its velocity carries it rapidly toward an edge. Conversely, the projection may temporarily leave the nominal support region while dynamic stepping can still recover the robot. Position, velocity, angular momentum, contact state, and future foothold feasibility must therefore be considered together.

Capture Point and Divergent Component of Motion provide useful indicators of dynamic recoverability. These quantities combine center-of-mass position and velocity to estimate where support must be created to arrest divergent motion. If the required capture location approaches or exceeds the reachable foothold region, the robot is entering a near-fall condition and should transition from nominal locomotion to emergency balance recovery.

Angular momentum is equally important because severe trunk rotation can make recovery impossible even when translational motion appears manageable. Large roll or pitch rates can rapidly drive the body toward terrain contact. A near-fall detector should therefore evaluate both linear and rotational states and estimate whether the available stance forces and future contacts can dissipate or redirect the accumulated momentum.

Contact degradation is another major cause of near-fall behavior. A foot may slip, lose normal force, land on an unexpected surface, or fail to establish the contact assumed by the gait planner. The feasible support region and contact-wrench set can then change almost instantaneously. Recovery logic must update the active contact model as soon as unreliable support is detected.

The first recovery action is often aggressive redistribution of ground reaction forces among the contacts that remain reliable. The controller can modify the desired whole-body wrench to oppose divergent center-of-mass motion and excessive body rotation. However, force redistribution is useful only while friction, normal-force, actuator, and joint-torque constraints still provide sufficient reserve authority.

When existing contacts cannot arrest the motion, stepping becomes necessary. Emergency foot placement should prioritize dynamic usefulness over preservation of the nominal gait pattern. A swing foot may be redirected toward a capture location, an intended foothold may be replaced, or a leg that was scheduled to remain in stance may be lifted if creating a new support point provides greater recovery capability.

Emergency stepping requires both spatial and temporal adaptation. The theoretically ideal foothold may be ineffective if the swing leg cannot reach it before the body state diverges further. The controller may shorten swing duration, increase swing-foot acceleration within actuator limits, reduce clearance when safe, or select another leg whose workspace permits faster establishment of a stabilizing contact.

Reachability places a hard limit on recovery. A desired capture location may lie beyond the kinematic workspace of every available leg. In this situation, the controller should select the best reachable foothold rather than command an impossible step. The first contact can reduce momentum sufficiently for a second step, making multi-step recovery preferable to an infeasible attempt at one-step stabilization.

Multi-step recovery is especially important after large disturbances or during fast locomotion. The first step may primarily prevent immediate collapse, while subsequent contacts progressively reduce center-of-mass velocity and angular momentum. Predictive planning can evaluate several future contact transitions and distribute recovery over them instead of demanding that a single foothold completely restore balance.

Body motion itself can contribute to recovery. Allowing the trunk to translate, lean, or rotate in a controlled manner can preserve leg reachability and reduce the required contact wrench. Attempting to keep the body rigidly at its nominal pose may consume valuable force authority. Near-fall control therefore treats body posture as a recovery variable rather than an invariant reference.

Base height can also be modified during emergency recovery. Lowering the body may reduce tipping sensitivity and prepare the legs for wider stabilizing contacts, while excessive lowering can consume workspace or risk body-ground collision. The appropriate response depends on terrain geometry, current leg configuration, vertical velocity, and the time remaining before possible impact.

Roll and pitch regulation should become recovery-aware. During normal locomotion, the controller may strongly track a desired trunk orientation, but during a near fall a temporary lean can be beneficial. Orientation objectives should therefore be softened when necessary so that contact forces can be used primarily to redirect momentum, after which the nominal body attitude can be restored progressively.

Centroidal dynamics provide a compact model for near-fall recovery because they represent how contact forces change total linear and angular momentum. A recovery optimizer can use this model to determine whether the remaining and planned contacts can generate sufficient impulse and moment. This enables direct reasoning about the quantities that determine whether the robot can avoid collapse.

Impulse capability is particularly relevant when little recovery time remains. A contact may be able to generate a large force, but only for a short duration before another transition occurs. The integral of force over available contact time determines how much momentum can be changed. Recovery planning should therefore consider both force magnitude and the duration for which that force can realistically be maintained.

Model Predictive Control is well suited to near-fall recovery because it evaluates future state evolution under constraints. MPC can predict center-of-mass motion, body rotation, contact forces, and contact transitions while optimizing emergency actions. It can determine whether force redistribution is sufficient, whether stepping is required, and which sequence of feasible contacts provides the best recovery opportunity.

The objective function used during emergency MPC should differ from nominal locomotion. Velocity tracking and gait regularity become less important, while momentum reduction, collision avoidance, feasible contact generation, and preservation of actuator reserve become dominant. Temporarily changing optimization weights allows the controller to use the robot\'s capabilities for survival rather than nominal performance.

Friction uncertainty must be handled conservatively because near-fall recovery often demands large tangential forces. A plan that depends on operating exactly at the estimated friction boundary is fragile. The optimizer should retain a safety margin when possible and avoid relying heavily on contacts that show evidence of slip, weak normal loading, uncertain terrain orientation, or poor contact geometry.

Terrain perception becomes increasingly important when emergency steps are required. A recovery foothold must not only be dynamically useful but also physically safe. Obstacles, holes, steep edges, unstable material, and large height discontinuities can invalidate an otherwise ideal capture location. Rapid terrain evaluation should therefore be integrated with emergency foothold generation.

Whole-Body Control executes the recovery strategy by coordinating base motion, stance forces, swing-leg trajectories, and joint torques. During a near fall, task hierarchy should change so that balance, contact integrity, and collision avoidance dominate secondary posture or locomotion objectives. Joint limits and torque saturation must remain enforced because unrealistic commands cannot recover the physical system.

Actuator saturation is a critical indicator of diminishing recovery authority. If several joints remain near their torque limits while the divergent motion continues to increase, the current strategy may no longer be sufficient. Monitoring torque reserve, contact-force margin, and leg workspace provides an estimate of how much corrective capability remains before upright recovery becomes physically infeasible.

Recovery should include explicit collision prediction. The trunk, knees, hips, or payload may approach the terrain during severe rotation or vertical collapse. Predicting likely impact locations allows the controller to modify body orientation or leg configuration to avoid contact when possible. If impact cannot be avoided, the strategy should transition from balance recovery toward damage-minimizing protective behavior.

The boundary between recoverable near fall and unavoidable fall is not fixed. It depends on gait phase, terrain, friction, speed, payload, available footholds, actuator capability, and the direction of disturbance. A useful recovery system therefore estimates a state-dependent viability or recoverability region rather than relying on one universal threshold for body angle or center-of-mass position.

Viability analysis asks whether at least one admissible sequence of future controls can keep the robot within safe states. Although exact viability computation for a full quadruped is expensive, approximate viability measures can be constructed from capture regions, reachable footholds, force feasibility, joint limits, and predicted collision. These measures provide a principled trigger for emergency recovery.

State-estimation latency becomes particularly dangerous near the recoverability boundary. A delayed estimate may describe a state that the robot has already left, causing the selected foothold or force command to be obsolete. High-rate inertial sensing, rapid contact detection, predictive filtering, and low-latency control execution are therefore essential for preserving the short time window available for recovery.

Recovery mode should not terminate immediately after one successful contact. The robot may remain dynamically unstable even though the immediate fall has been prevented. The controller should monitor momentum, contact margins, body orientation, and future support feasibility until the state has returned to a sufficiently robust region before resuming the nominal gait and velocity command.

Transition back to normal locomotion should be gradual. Recovery steps can leave the feet in highly asymmetric locations and the body away from its preferred posture. A stabilization phase can reduce residual velocity, redistribute load, restore base height and orientation, and reposition the feet. Only after adequate margins are recovered should the nominal gait generator regain full authority.

Payloads and manipulators can substantially modify the near-fall boundary. A high or offset payload increases rotational sensitivity, while manipulator motion can either worsen or assist recovery by changing angular momentum and center-of-mass location. Whole-body recovery should therefore consider movable upper-body components as controllable resources when their motion can safely increase recoverability.

Learning-based recovery policies can complement model-based methods by discovering coordinated actions that are difficult to design manually. Simulation can expose the robot to pushes, slips, missed footholds, terrain errors, actuator degradation, and combinations of disturbances near the fall boundary. The learned policy can propose rapid actions while model-based constraints enforce contact, torque, and collision safety.

Training should include states that are rarely encountered during successful nominal locomotion. If learning data contain only mild disturbances, the policy will have little experience with large body angles, high angular velocity, unusual contact patterns, or extreme joint configurations. Purposeful near-fall state sampling and curriculum design can therefore expand the range of recoverable situations.

Evaluation should measure more than fall rate. Useful metrics include the recoverable disturbance envelope, minimum remaining stability margin, maximum body angle, peak angular velocity, number of recovery steps, recovery distance, actuator saturation, contact slip, collision occurrence, and time required to return to a robust locomotion state.

Experiments should generate near-fall conditions through controlled pushes, sudden foothold loss, low-friction patches, unexpected terrain height, payload shifts, and contact failures. Testing should cover different gait phases and disturbance directions because the same external impulse can be easily recoverable in one contact configuration but unrecoverable in another.

Balance recovery from a near-fall state is ultimately a problem of preserving future control possibilities. The robot must recognize when nominal stabilization is becoming insufficient, exploit remaining contact and actuator authority, create new support where necessary, and temporarily sacrifice gait tracking or posture accuracy to keep the system inside a recoverable region.

A capable quadruped therefore treats falling as a dynamic process rather than a binary event. By combining recoverability estimation, momentum regulation, emergency force redistribution, adaptive stepping, predictive contact planning, whole-body control, and protective fallback behavior, the robot can intervene during the narrow interval between ordinary disturbance rejection and unavoidable physical collapse.

## 05.10. Balance Controller Benchmark Push Recovery Test

![](images/image10.png){width="7.268055555555556in" height="7.268055555555556in"}

A push-recovery benchmark evaluates whether a quadruped balance controller can maintain or restore a recoverable state after controlled external disturbances. Unlike nominal walking tests, the benchmark deliberately drives the robot away from its planned motion and measures how effectively estimation, contact-force control, stepping, and whole-body coordination prevent a fall and restore stable locomotion.

A useful benchmark must define the disturbance in physically measurable terms. Pushes can be characterized by force magnitude, duration, impulse, direction, application point, and timing relative to the gait cycle. Reporting only the peak force is insufficient because a short high-force impact and a longer moderate-force push can transfer very different amounts of momentum to the robot.

Impulse provides an important common measure because it represents the time integral of applied force and directly relates to the change in linear momentum. For rotational disturbances, the application point must also be recorded because the same force can generate different angular impulses. A complete benchmark therefore documents both the applied force history and its location relative to the robot body.

Disturbances should be applied using a repeatable mechanism rather than uncontrolled manual pushing whenever quantitative comparison is required. A calibrated linear actuator, pendulum impactor, instrumented pushing device, or controlled suspended mass can generate reproducible disturbances. Force sensors or load cells should measure the actual interaction instead of assuming that the commanded disturbance equals the force delivered.

The test should cover multiple disturbance directions. Longitudinal pushes evaluate forward and backward recovery, lateral pushes examine roll stability and side stepping, and oblique pushes require simultaneous regulation of multiple motion components. Vertical or combined disturbances can additionally evaluate contact unloading and the controller\'s ability to preserve reliable ground contact.

The point of force application should also vary. A force applied near the center of mass primarily changes linear momentum, while a force applied higher on the trunk can create substantial roll or pitch angular momentum. Applying disturbances at several known heights and body locations helps separate translational recovery performance from rotational stabilization capability.

Push timing is particularly important during locomotion because the available support geometry changes continuously. A disturbance during four-leg support can be much easier to reject than the same disturbance during a two-leg diagonal stance. Benchmark trials should therefore synchronize push timing with gait phase or record the exact contact configuration when the disturbance begins.

Standing tests provide a useful baseline because they isolate balance control from gait transitions. The robot can be subjected to progressively stronger pushes while maintaining a fixed nominal stance. These trials reveal force-redistribution capability, friction limitations, body compliance, and the disturbance level at which recovery stepping first becomes necessary.

Walking and trotting tests extend the benchmark to dynamic locomotion. Pushes should be applied at representative gait phases and commanded velocities because recovery authority depends on existing momentum and contact timing. The controller should be evaluated not only on whether the robot avoids falling, but also on how effectively it returns to a controllable locomotion state.

A benchmark should distinguish in-place recovery from stepping recovery. For small disturbances, the controller may reject the push through contact-force redistribution and body motion without changing footholds. Larger disturbances may require one or more recovery steps. Recording the transition between these strategies provides information about the effective disturbance-rejection range of the controller.

The maximum recoverable disturbance is a central metric but requires a precise definition. Recovery can be defined as avoiding body-ground collision and returning to a specified bounded state within a fixed time. The maximum recoverable impulse can then be estimated by gradually increasing disturbance severity until repeated trials no longer satisfy the recovery criterion.

Because recovery has stochastic elements, a single successful trial should not define the limit. Small differences in contact, friction, state estimation, or actuator temperature can change the result near the stability boundary. Each disturbance condition should therefore be repeated, and recovery probability should be reported as a function of impulse or force magnitude.

Center-of-mass displacement provides a useful measure of how much the robot yields before recovering. Peak displacement, displacement at the end of the push, and total recovery distance can be recorded. A controller that remains upright but travels a large uncontrolled distance may be less effective than one that dissipates the disturbance within a compact region.

Body orientation should be measured throughout the test. Maximum roll and pitch excursions indicate how strongly the trunk departs from its nominal pose, while peak angular velocity provides information about rotational disturbance severity. Settling time can describe how quickly orientation returns to an acceptable range after the disturbance has ended.

Contact-force measurements reveal how the controller physically produces recovery. Peak normal force, tangential force, load redistribution, and friction utilization can be recorded for each foot. These signals show whether recovery depends on balanced use of the available contacts or repeatedly drives particular legs close to friction or actuator limits.

Friction margin is a particularly valuable metric because a successful trial performed near the slip boundary may have little robustness to terrain uncertainty. Estimated or measured contact forces can be compared with the available friction region. Controllers that preserve larger margins while achieving comparable recovery generally possess greater reserve capability.

Foot slip should be detected explicitly rather than inferred only from a final fall. Relative foot motion, contact-force behavior, and kinematic inconsistency can identify partial or temporary slip. The number, duration, and magnitude of slip events provide important information because a controller may recover successfully while repeatedly violating the assumed rigid-contact model.

Recovery-step behavior should be quantified when stepping occurs. Useful measures include step initiation delay, touchdown time, step length, step direction, number of recovery steps, and deviation from the nominal foothold. These measurements reveal whether the controller creates new support rapidly and whether its foot-placement strategy is consistent with the direction of disturbed momentum.

Capture Point or Divergent Component of Motion can provide state-based benchmark quantities. The distance between the estimated capture state and the feasible support or foothold region indicates how close the robot approaches the recoverability boundary. Tracking this value throughout the trial can explain why apparently similar disturbances produce different recovery outcomes.

Actuator utilization should be monitored because successful recovery obtained through prolonged saturation may not generalize to repeated disturbances. Peak joint torque, torque-rate demand, motor current, velocity, and saturation duration can be recorded. Thermal state should also be controlled or reported when repeated high-force trials significantly heat the actuators.

State-estimation performance should be evaluated alongside mechanical recovery. The benchmark can compare estimated base velocity, orientation, contact state, and external wrench against reference measurements when available. Detection latency is especially important because delayed disturbance recognition can consume the limited time available for force redistribution or emergency stepping.

An external motion-capture system can provide reference body position and orientation during laboratory testing. Force plates or instrumented feet can provide reference ground reaction forces, while the disturbance device measures applied force. Time synchronization among these systems is essential so that the causal sequence from push to estimation, control action, and recovery can be reconstructed accurately.

Controller latency should be included in the benchmark. The time between disturbance onset, disturbance detection, modified force command, swing-foot replanning, and physical actuator response can be measured. Breaking recovery into these stages helps identify whether limitations arise from sensing, estimation, optimization, communication, or actuator dynamics.

Terrain conditions should be standardized for baseline comparisons. Surface material, friction coefficient, slope, compliance, and irregularity influence recovery performance. A controller tested only on high-friction laboratory flooring may appear substantially stronger than it is in practical environments. Additional trials should therefore progressively introduce lower friction and uneven terrain.

Payload variation provides another important benchmark dimension. Tests can be repeated with nominal mass, increased payload, shifted center of mass, or elevated payload configurations. The controller should either adapt its dynamic model or demonstrate sufficient robustness to parameter variation. Reporting payload conditions prevents misleading comparisons between mechanically different test cases.

Recovery tests should also include unexpected contact events. A stance foot can be placed on a low-friction patch, a planned foothold can be removed, or a swing foot can encounter an obstacle. These tests evaluate whether the balance controller can handle disturbances that arise from contact-model failure rather than from a direct external push.

Near-fall tests can extend the benchmark toward the controller\'s viability boundary. Disturbance magnitude is increased until the robot requires aggressive stepping, large body motion, or multiple recovery contacts. These trials reveal how the controller behaves when nominal posture tracking becomes secondary to preservation of recoverability.

Safety mechanisms are essential during high-energy testing. A passive overhead tether or fall-arrest system can prevent hardware damage without significantly supporting the robot during normal motion. The tether should remain slack during valid trials so that it does not contribute stabilizing forces that would artificially improve the measured recovery performance.

A consistent failure criterion is necessary. Failure may be declared when the trunk or protected body component contacts the ground, when the safety tether carries significant load, when the robot leaves the designated test area, or when the controller cannot return to a bounded stable state within the specified recovery interval. These conditions should be defined before testing begins.

Benchmark results can be summarized as a recovery envelope rather than a single maximum force. The envelope can describe successful disturbance combinations across direction, impulse, gait phase, speed, payload, and terrain condition. This representation better captures the multidimensional nature of quadruped balance capability and exposes directions or operating states with weak recovery performance.

Statistical reporting improves comparability. For each test condition, the number of trials, success rate, mean response, variability, and confidence interval can be reported. Near the failure boundary, logistic or similar probabilistic models can estimate the disturbance magnitude corresponding to selected recovery probabilities instead of treating the limit as a perfectly sharp threshold.

Controller comparisons should use identical mechanical and environmental conditions whenever possible. Different robot mass, foot geometry, actuator strength, stance width, or friction can dominate the result and obscure algorithmic differences. When comparing controllers on the same platform, initial state, gait, disturbance device, terrain, and evaluation criteria should remain consistent.

Ablation tests can reveal which controller components contribute most strongly to recovery. Trials may compare force redistribution alone with stepping enabled, nominal feedback with disturbance feedforward, or fixed footholds with predictive replanning. Such comparisons transform the benchmark from a demonstration of success into an engineering tool for understanding controller architecture.

Simulation can support benchmark development before hardware testing. Identical disturbance protocols can be applied across large parameter ranges to identify critical gait phases, likely failure modes, and suitable hardware test levels. However, simulation results should not replace physical validation because real contact, actuator limits, latency, compliance, and friction uncertainty strongly affect push recovery.

A rigorous push-recovery benchmark therefore measures the complete response from disturbance application to restoration of a robust state. It evaluates disturbance magnitude, momentum change, body motion, contact forces, stepping behavior, actuator utilization, estimation latency, and final recovery rather than reducing performance to a simple fall-or-no-fall result.

By standardizing disturbance generation, gait phase, environmental conditions, success criteria, and quantitative metrics, push-recovery testing provides a reproducible method for evaluating quadruped balance controllers. The resulting recovery envelope reveals not only whether the robot survives a push, but how much physical and control margin remains while it returns to stable operation.
